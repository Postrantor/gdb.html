---
tip: translate by openai@2023-06-24 01:07:47
...
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

> 类型定义在自我描述中可以从基本构件组合出复合类型，但不能定义基本类型。相反，[GDB]提供了基本类型的标准标识符。当前支持的类型是：

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

> 指向未指定的代码和数据的指针。程序计数器和任何专用返回地址寄存器可以标记为代码指针；打印代码指针将其转换为符号地址。堆栈指针和任何专用地址寄存器可以标记为数据指针。

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
