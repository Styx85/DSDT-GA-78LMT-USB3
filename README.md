````markdown
# DSDT fixes for Gigabyte GA-78LMT-USB3

Updated ACPI DSDT fixes for the **Gigabyte GA-78LMT-USB3 Rev. 4.1** running **BIOS F4 (2012-10-19)**.

This repository was originally created in 2017 to make the board's firmware DSDT compile cleanly with `iasl`.

The fixes were revisited in 2026 using a fresh DSDT extracted from the same board and BIOS.

## Repository layout

- `dsdt.dsl`  
  Current corrected DSDT source.

- `dsdt.aml`  
  Compiled AML generated from the current `dsdt.dsl` using ACPICA/iasl 20251212.

- `reference/dsdt-bios-f4-raw.dsl`  
  Freshly extracted and decompiled BIOS F4 DSDT without manual fixes.

- `legacy/dsdt-2017.dsl`  
  Historical corrected DSDT from the original 2017 work.

The included `dsdt.aml` is the reference build corresponding to the current `dsdt.dsl`.

## Hardware

Tested on:

- Gigabyte GA-78LMT-USB3
- Revision 4.1
- Award BIOS F4
- BIOS release date: 2012-10-19

This repository is therefore **not specifically for GA-78LMT-USB3 Rev. 6.0 / BIOS F2**.

Other board revisions may contain substantially different ACPI tables and should not use this DSDT without comparing against their own firmware tables first.

## Extract the firmware DSDT

On Linux:

```bash
sudo cat /sys/firmware/acpi/tables/DSDT > dsdt.aml
iasl -d dsdt.aml
````

This produces a decompiled `dsdt.dsl`.

Always keep the untouched firmware dump for comparison before applying fixes.

## Build

Compile the corrected source with:

```bash
iasl dsdt.dsl
```

This produces `dsdt.aml`.

The repository includes the AML generated from the current corrected source so that the published source and reference build remain aligned.

Current reference build:

```text
Intel ACPI Component Architecture
ASL+ Optimizing Compiler/Disassembler version 20251212

Compilation successful.
0 Errors, 10 Warnings, 73 Remarks, 981 Optimizations, 2 Constants Folded
```

The exact input byte count may change when the source header or comments are adjusted; the compiler result above is the relevant validation state.

## ACPI table revision for Linux override

The original BIOS DSDT identifies itself as:

```text
OEM ID           "GBT   "
OEM Table ID     "GBTUACPI"
OEM Revision     0x00001000
```

The corrected DSDT keeps the same OEM ID and OEM Table ID but increments the OEM revision to:

```text
0x00001001
```

The current `DefinitionBlock` therefore uses:

```asl
DefinitionBlock ("", "DSDT", 1, "GBT   ", "GBTUACPI", 0x00001001)
```

This is intentional.

Linux ACPI initrd table override treats the replacement table as an upgrade of the firmware table. Keeping the same table identity while using a higher OEM revision allows the corrected DSDT to replace the original BIOS F4 DSDT during early boot.

## Applied fixes

The 2026 refresh was recreated from a fresh BIOS F4 DSDT instead of simply reusing the 2017 source.

The current fixes include:

### Resource descriptor fixes

Several ACPI resource descriptors expose 16-bit `_MIN` and `_MAX` fields while the firmware source accesses them using `CreateByteField`.

These have been changed to `CreateWordField` where appropriate, including the FDC, UART, LPT and ECP resource methods.

### Invalid resource lengths

Several resource descriptors produced invalid length/minimum/maximum combinations when recompiled.

The corrected values include:

```text
PCI0 memory window:
0xFFF00000 -> 0xFEB00000

PMIO fixed memory resource:
0x00000000 -> 0x00000001

PMIO memory window:
0x00000BFF -> 0x00000C00
```

These values also correspond to the fixes present in the original 2017 version.

### Serialized control methods

The firmware creates named ACPI objects from a number of control methods declared as `NotSerialized`.

Methods identified by current ACPICA as requiring serialization have been changed to `Serialized`.

This applies to, among others:

* AMD AOD/WMI methods
* PCI resource methods
* SATA power/status methods
* IDE timing methods
* legacy device `_CRS` methods

The same class of fixes was already present in the 2017 version.

### WMAA return value

The firmware `WMAA` method does not return a value on every control path.

A default return package is added:

```asl
Return (Package (0x02)
{
    Zero,
    Zero
})
```

### _WAK return value

`_WAK` is a reserved ACPI method and is expected to return an Integer or Package.

The firmware method lacks that return value, so the corrected version restores:

```asl
Return (Package (0x02)
{
    Zero,
    Zero
})
```

### PEWS self-assignment

The decompiler currently produces:

```asl
\PEWS = \PEWS
```

which ACPICA warns about as a source/target self-assignment.

The corrected version preserves the original value through a temporary local variable:

```asl
Local1 = \PEWS
\PEWS = Local1
```

## Remaining compiler warnings

The current source intentionally retains 10 warnings.

Eight are caused by the legacy ACPI 1.0-style processor declarations:

```text
Legacy Processor() keyword detected. Use Device() keyword instead.
```

The BIOS defines eight processors using the old `Processor()` object.

These are left unchanged because converting old firmware CPU objects to modern `Device()` objects would be a much more invasive semantic change than the fixes performed by this repository.

Two additional firmware warnings are currently retained:

```text
Device object requires either a _HID or _ADR, but not both
```

for `PCI0`, and:

```text
Method Local is set but never used
```

for the firmware's `CondRefOf (\_OSI, Local0)` construct.

Neither is modified solely to obtain a zero-warning compiler result.

## Remarks

Current ACPICA also reports remarks for:

* named objects created inside methods,
* unused method arguments,
* temporary fields that are not subsequently referenced.

These are not compilation errors and are intentionally not rewritten just to reduce the compiler message count.

Changing them would require substantially more invasive restructuring of the original firmware AML.

## AOD / WMI and `_WDG`

The board exposes an AMD AOD device with:

```asl
_HID = "PNP0C14"
```

and an ACPI `_WDG` object.

`PNP0C14` represents a Windows Management Instrumentation (WMI) ACPI device, and `_WDG` contains its WMI GUID descriptors.

The `_WDG` object was already present in the original 2017 DSDT and is intentionally retained.

It should **not** be confused with the ACPI WDAT watchdog table or automatically assumed to be related to Linux's `sp5100_tco` watchdog driver.

Renaming or disabling `_WDG` is therefore not part of the current DSDT fix set.

## Linux watchdog note

On the test system, modern Linux currently reports:

```text
sp5100_tco: SP5100/SB800 TCO WatchDog Timer Driver
sp5100-tco: Failed to reserve MMIO or alternate MMIO region
sp5100-tco: probe with driver sp5100-tco failed with error -16
```

This issue is still under investigation.

The nearby ACPI warning concerning the SystemIO region around `0xB00` belongs to the firmware's SMBus operation region (`SOR1`) and has not been demonstrated to be the resource collision responsible for the `sp5100_tco` failure.

No speculative `_WDG` or `SOR1` modification is included in this repository.

## Linux initrd ACPI override

The corrected `dsdt.aml` can be loaded through an early initrd ACPI table override.

On Arch Linux with `mkinitcpio`, copy the compiled AML to:

```bash
sudo mkdir -p /etc/initcpio/acpi_override
sudo cp dsdt.aml /etc/initcpio/acpi_override/dsdt.aml
```

Add the `acpi_override` hook to the existing `HOOKS` array in:

```text
/etc/mkinitcpio.conf
```

Do not replace the existing hooks; only add `acpi_override`.

Then rebuild the initramfs:

```bash
sudo mkinitcpio -P
```

The table can be checked inside the generated initramfs with:

```bash
lsinitcpio /boot/initramfs-linux.img | grep -i -E 'acpi|dsdt'
```

The expected path is:

```text
kernel/firmware/acpi/dsdt.aml
```

After rebooting, verify that Linux loaded the replacement table:

```bash
sudo dmesg | grep -i -E 'ACPI.*override|ACPI.*upgrade|DSDT'
```

Always keep a working boot fallback when experimenting with custom ACPI tables.

## Historical note

The original 2017 version compiled with:

```text
iasl 20170929

0 Errors
16 Warnings
26 Remarks
38 Optimizations
```

Many of the fixes independently rediscovered using current ACPICA match the corrections made in that original version.

The historical source is retained in:

```text
legacy/dsdt-2017.dsl
```

## Kernel ACPI OS identification

The original 2017 setup used:

```text
acpi_os_name='Windows 2001'
```

because some firmware paths depended on the operating-system identification presented through ACPI.

This is retained here as historical information rather than as a general recommendation for current Linux systems.

If required for a particular setup, verify the resulting ACPI behaviour on that system rather than adding it blindly.

## Disclaimer

ACPI tables directly describe and control platform hardware.

Do not use the compiled DSDT from this repository blindly on a different motherboard revision, BIOS version or system.

Extract your own firmware DSDT, compare it against the reference table, understand the changes, and keep a working boot fallback before loading a custom ACPI table.

````
