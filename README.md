# DSDT-GA-78LMT-USB3
**Try to FixUp GA-78LMT-USB3 DSDT Table**



Latest compiler run is down to 0 Errors, 16 Warnings, 26 Remarks and 38 Optimizations. DSDT table is up and running again.
It is important to set kernel boot line options explicitly to acpi_os_name='Windows 2001' to use all functions.



>Intel ACPI Component Architecture
>ASL+ Optimizing Compiler/Disassembler version 20170929
>Copyright (c) 2000 - 2017 Intel Corporation
>
>dsdt.dsl    317:     Method (TRMD, 1, NotSerialized)
>Warning  4089 -                ^ Object is not referenced
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
>dsdt.dsl    700:             Method (DISC, 0, NotSerialized)
>Warning  4089 -                        ^ Object is not referenced
>
>dsdt.dsl    720:             Method (WROW, 4, Serialized)
>Warning  4089 -                        ^ Object is not referenced
>
>dsdt.dsl    754:             Method (GROW, 4, Serialized)
>Warning  4089 -                        ^ Object is not referenced
>
>dsdt.dsl    823:             Method (CBTP, 1, Serialized)
>Warning  4089 -                        ^ Object is not referenced
>
>dsdt.dsl    859:             Method (ABS, 2, NotSerialized)
>Warning  4089 -                       ^ Object is not referenced
>
>dsdt.dsl    871:             Name (EXBF, Buffer (0x78){})
>Warning  4089 -                      ^ Object is not referenced
>
>dsdt.dsl    898:             Method (GCMS, 1, Serialized)
>Warning  4089 -                        ^ Object is not referenced
>
>dsdt.dsl    916:             Method (SCMS, 2, Serialized)
>Warning  4089 -                        ^ Object is not referenced
>
>dsdt.dsl   1359:                 CreateDWordField (INFO, Zero, IFID)
>Remark   2089 -                         Object is not referenced ^  (Name [IFID] is within a method [AM05])
>
>dsdt.dsl   1360:                 CreateDWordField (INFO, 0x04, IFMI)
>Remark   2089 -                         Object is not referenced ^  (Name [IFMI] is within a method [AM05])
>
>dsdt.dsl   1361:                 CreateDWordField (INFO, 0x08, IFMX)
>Remark   2089 -                         Object is not referenced ^  (Name [IFMX] is within a method [AM05])
>
>dsdt.dsl   1362:                 CreateDWordField (INFO, 0x0C, IFSP)
>Remark   2089 -                         Object is not referenced ^  (Name [IFSP] is within a method [AM05])
>
>dsdt.dsl   1363:                 CreateField (INFO, 0x80, 0x03, IFST)
>Remark   2089 -                          Object is not referenced ^  (Name [IFST] is within a method [AM05])
>
>dsdt.dsl   1574:             Name (WQBA, Buffer (0x0BBB)
>Warning  4089 -                      ^ Object is not referenced
>
>dsdt.dsl   1963:             Method (WMAA, 3, NotSerialized)
>Warning  4089 -                        ^ Object is not referenced
>
>dsdt.dsl   2262:         Method (SMOD, 1, NotSerialized)
>Remark   2146 -                    ^ Method Argument is never used (Arg0)
>
>dsdt.dsl   2262:         Method (SMOD, 1, NotSerialized)
>Warning  4089 -                    ^ Object is not referenced
>
>dsdt.dsl   2319:                     If (CondRefOf (\_OSI, Local0))
>Warning  3144 -             Method Local is set but never used ^  (Local0)
>
>dsdt.dsl   4733:                     Name (ATT3, ResourceTemplate ()
>Warning  4089 -     Object is not referenced ^ 
>
>dsdt.dsl   5027:                 Method (STM, 3, Serialized)
>Remark   2146 -                           ^ Method Argument is never used (Arg1)
>
>dsdt.dsl   5027:                 Method (STM, 3, Serialized)
>Remark   2146 -                           ^ Method Argument is never used (Arg2)
>
>dsdt.dsl   6232:                 Method (DISD, 1, NotSerialized)
>Remark   2146 -                            ^ Method Argument is never used (Arg0)
>
>dsdt.dsl   6236:                 Method (CKIO, 2, NotSerialized)
>Remark   2146 -                            ^ Method Argument is never used (Arg0)
>
>dsdt.dsl   6236:                 Method (CKIO, 2, NotSerialized)
>Remark   2146 -                            ^ Method Argument is never used (Arg1)
>
>dsdt.dsl   6240:                 Method (SLDM, 2, NotSerialized)
>Remark   2146 -                            ^ Method Argument is never used (Arg0)
>
>dsdt.dsl   6240:                 Method (SLDM, 2, NotSerialized)
>Remark   2146 -                            ^ Method Argument is never used (Arg1)
>
>dsdt.dsl   6309:                 Method (GSRG, 1, NotSerialized)
>Warning  4089 -   Object is not referenced ^ 
>
>dsdt.dsl   6315:                 Method (SSRG, 2, NotSerialized)
>Warning  4089 -   Object is not referenced ^ 
>
>dsdt.dsl   6377:                     CreateWordField (BUF0, \_SB.PCI0.FDC0._CRS._Y02._MIN, IOLO)  // _MIN: Minimum Base Address
>Remark   2089 -                                                     Object is not referenced ^  (Name [IOLO] is within a method [_CRS])
>
>dsdt.dsl   6378:                     CreateByteField (BUF0, 0x03, IOHI)
>Remark   2089 -                            Object is not referenced ^  (Name [IOHI] is within a method [_CRS])
>
>dsdt.dsl   6379:                     CreateWordField (BUF0, \_SB.PCI0.FDC0._CRS._Y02._MAX, IORL)  // _MAX: Maximum Base Address
>Remark   2089 -                                                     Object is not referenced ^  (Name [IORL] is within a method [_CRS])
>
>dsdt.dsl   6380:                     CreateByteField (BUF0, 0x05, IORH)
>Remark   2089 -                            Object is not referenced ^  (Name [IORH] is within a method [_CRS])
>
>dsdt.dsl   6411:                     CreateByteField (Arg0, 0x02, IOLO)
>Remark   2089 -                            Object is not referenced ^  (Name [IOLO] is within a method [_SRS])
>
>dsdt.dsl   6412:                     CreateByteField (Arg0, 0x03, IOHI)
>Remark   2089 -                            Object is not referenced ^  (Name [IOHI] is within a method [_SRS])
>
>dsdt.dsl   6414:                     CreateWordField (Arg0, 0x19, IRQW)
>Remark   2089 -                            Object is not referenced ^  (Name [IRQW] is within a method [_SRS])
>
>dsdt.dsl   6415:                     CreateByteField (Arg0, 0x1C, DMAV)
>Remark   2089 -                            Object is not referenced ^  (Name [DMAV] is within a method [_SRS])
>
>dsdt.dsl   6682:                     CreateByteField (Arg0, 0x04, IORL)
>Remark   2089 -                            Object is not referenced ^  (Name [IORL] is within a method [_SRS])
>
>dsdt.dsl   6683:                     CreateByteField (Arg0, 0x05, IORH)
>Remark   2089 -                            Object is not referenced ^  (Name [IORH] is within a method [_SRS])
>
>ASL Input:     dsdt.dsl - 7343 lines, 259136 bytes, 2441 keywords
>AML Output:    dsdt.aml - 25010 bytes, 786 named objects, 1655 executable opcodes
>Hex Dump:      dsdt.hex - 234857 bytes
>
>Compilation complete. 0 Errors, 16 Warnings, 26 Remarks, 38 Optimizations

