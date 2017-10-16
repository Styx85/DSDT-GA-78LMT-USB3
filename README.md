# DSDT-GA-78LMT-USB3
**Try to FixUp GA-78LMT-USB3 DSDT Table**



Latest compiler run is down to 1 warning and 26 remarks. DSDT table is up and running again.
It is important to set kernel boot line options explicitly to acpi_os_name='Windows 2009' to use all functions.



>Intel ACPI Component Architecture
>ASL+ Optimizing Compiler/Disassembler version 20170303
>Copyright (c) 2000 - 2017 Intel Corporation
>
>dsdt.dsl    684:             Method (BM05, 1, NotSerialized)
>Remark   2146 -                        ^ Method Argument is never used (Arg0)
>
>dsdt.dsl    688:             Method (EM05, 1, NotSerialized)
>Remark   2146 -                        ^ Method Argument is never used (Arg0)
>
>dsdt.dsl    696:             Method (HM07, 1, NotSerialized)
>Remark   2146 -                        ^ Method Argument is never used (Arg0)
>
>dsdt.dsl   1360:                 CreateDWordField (INFO, 0x00, IFID)
>Remark   2089 -                         Object is not referenced ^  (Name [IFID] is within a method [AM05])
>
>dsdt.dsl   1361:                 CreateDWordField (INFO, 0x04, IFMI)
>Remark   2089 -                         Object is not referenced ^  (Name [IFMI] is within a method [AM05])
>
>dsdt.dsl   1362:                 CreateDWordField (INFO, 0x08, IFMX)
>Remark   2089 -                         Object is not referenced ^  (Name [IFMX] is within a method [AM05])
>
>dsdt.dsl   1363:                 CreateDWordField (INFO, 0x0C, IFSP)
>Remark   2089 -                         Object is not referenced ^  (Name [IFSP] is within a method [AM05])
>
>dsdt.dsl   1364:                 CreateField (INFO, 0x80, 0x03, IFST)
>Remark   2089 -                          Object is not referenced ^  (Name [IFST] is within a method [AM05])
>
>dsdt.dsl   2253:         Method (SMOD, 1, NotSerialized)
>Remark   2146 -                    ^ Method Argument is never used (Arg0)
>
>dsdt.dsl   2310:                     If (CondRefOf (\_OSI, Local0))
>Warning  3144 -             Method Local is set but never used ^  (Local0)
>
>dsdt.dsl   5017:                 Method (STM, 3, Serialized)
>Remark   2146 -                           ^ Method Argument is never used (Arg1)
>
>dsdt.dsl   5017:                 Method (STM, 3, Serialized)
>Remark   2146 -                           ^ Method Argument is never used (Arg2)
>
>dsdt.dsl   6222:                 Method (DISD, 1, NotSerialized)
>Remark   2146 -                            ^ Method Argument is never used (Arg0)
>
>dsdt.dsl   6226:                 Method (CKIO, 2, NotSerialized)
>Remark   2146 -                            ^ Method Argument is never used (Arg0)
>
>dsdt.dsl   6226:                 Method (CKIO, 2, NotSerialized)
>Remark   2146 -                            ^ Method Argument is never used (Arg1)
>
>dsdt.dsl   6230:                 Method (SLDM, 2, NotSerialized)
>Remark   2146 -                            ^ Method Argument is never used (Arg0)
>
>dsdt.dsl   6230:                 Method (SLDM, 2, NotSerialized)
>Remark   2146 -                            ^ Method Argument is never used (Arg1)
>
>dsdt.dsl   6367:                     CreateWordField (BUF0, \_SB.PCI0.FDC0._CRS._Y02._MIN, IOLO)  /* _MIN: Minimum Base Address
>Remark   2089 -                                                     Object is not referenced ^  (Name [IOLO] is within a method [_CRS])
>
>dsdt.dsl   6368:                     CreateByteField (BUF0, 0x03, IOHI)
>Remark   2089 -                            Object is not referenced ^  (Name [IOHI] is within a method [_CRS])
>
>dsdt.dsl   6369:                     CreateWordField (BUF0, \_SB.PCI0.FDC0._CRS._Y02._MAX, IORL)  /* _MAX: Maximum Base Address
>Remark   2089 -                                                     Object is not referenced ^  (Name [IORL] is within a method [_CRS])
>
>dsdt.dsl   6370:                     CreateByteField (BUF0, 0x05, IORH)
>Remark   2089 -                            Object is not referenced ^  (Name [IORH] is within a method [_CRS])
>
>dsdt.dsl   6401:                     CreateByteField (Arg0, 0x02, IOLO)
>Remark   2089 -                            Object is not referenced ^  (Name [IOLO] is within a method [_SRS])
>
>dsdt.dsl   6402:                     CreateByteField (Arg0, 0x03, IOHI)
>Remark   2089 -                            Object is not referenced ^  (Name [IOHI] is within a method [_SRS])
>
>dsdt.dsl   6404:                     CreateWordField (Arg0, 0x19, IRQW)
>Remark   2089 -                            Object is not referenced ^  (Name [IRQW] is within a method [_SRS])
>
>dsdt.dsl   6405:                     CreateByteField (Arg0, 0x1C, DMAV)
>Remark   2089 -                            Object is not referenced ^  (Name [DMAV] is within a method [_SRS])
>
>dsdt.dsl   6672:                     CreateByteField (Arg0, 0x04, IORL)
>Remark   2089 -                            Object is not referenced ^  (Name [IORL] is within a method [_SRS])
>
>dsdt.dsl   6673:                     CreateByteField (Arg0, 0x05, IORH)
>Remark   2089 -                            Object is not referenced ^  (Name [IORH] is within a method [_SRS])
>
>ASL Input:     dsdt.dsl - 7332 lines, 259894 bytes, 2445 keywords
>AML Output:    dsdt.aml - 25010 bytes, 786 named objects, 1659 executable opcodes
>Hex Dump:      dsdt.hex - 234857 bytes
>
>Compilation complete. 0 Errors, 1 Warnings, 26 Remarks, 983 Optimizations, 2 Constants Folded
