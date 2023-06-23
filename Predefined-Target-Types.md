---
description: Predefined Target Types (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Predefined Target Types (Debugging with GDB)
lang: en
resource-type: document
title: Predefined Target Types (Debugging with GDB)
---
::: header
Next: [Enum Target Types](Enum-Target-Types.html#Enum-Target-Types)]
:::

---

### G.3 Predefined Target Types

Type definitions in the self-description can build up composite types from basic building blocks, but can not define fundamental types. Instead, standard identifiers are provided by [GDB] for the fundamental types. The currently supported types are:

`bool`

:   Boolean type, occupying a single bit.

`int8`
`int16`
`int24`
`int32`
`int64`
`int128`

:   Signed integer types holding the specified number of bits.

`uint8`
`uint16`
`uint24`
`uint32`
`uint64`
`uint128`

:   Unsigned integer types holding the specified number of bits.

`code_ptr`
`data_ptr`

:   Pointers to unspecified code and data. The program counter and any dedicated return address register may be marked as code pointers; printing a code pointer converts it into a symbolic address. The stack pointer and any dedicated address registers may be marked as data pointers.

`ieee_half`

:   Half precision IEEE floating point.

`ieee_single`

:   Single precision IEEE floating point.

`ieee_double`

:   Double precision IEEE floating point.

`bfloat16`

:   The 16-bit *brain floating point* format used e.g. by x86 and ARM.

`arm_fpa_ext`

:   The 12-byte extended precision format used by ARM FPA registers.

`i387_ext`

:   The 10-byte extended precision format used by x87 registers.

`i386_eflags`

:   32bit [EFLAGS] register used by x86.

`i386_mxcsr`

:   32bit [MXCSR] register used by x86.
