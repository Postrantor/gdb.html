---
tip: translate by openai@2023-06-23 20:28:06
...
---
description: Decimal Floating Point (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Decimal Floating Point (Debugging with GDB)
lang: en
resource-type: document
title: Decimal Floating Point (Debugging with GDB)
---
::: header
Previous: [Debugging C Plus Plus](Debugging-C-Plus-Plus.html#Debugging-C-Plus-Plus)]
:::

---

#### 15.4.1.8 Decimal Floating Point format


[GDB] can examine, set and perform computations with numbers in decimal floating point format, which in the C language correspond to the `_Decimal32`, `_Decimal64` and `_Decimal128` types as specified by the extension to support decimal floating-point arithmetic.

> GDB可以检查、设置和执行十进制浮点格式的数字计算，在C语言中，这些数字对应于“_Decimal32”、“_Decimal64”和“_Decimal128”类型，这些类型是用来支持十进制浮点算术的扩展。


There are two encodings in use, depending on the architecture: BID (Binary Integer Decimal) for x86 and x86-64, and DPD (Densely Packed Decimal) for PowerPC and S/390. [GDB] will use the appropriate encoding for the configured target.

> 根据架构不同，有两种编码方式：x86和x86-64使用BID（二进制整数十进制），PowerPC和S/390使用DPD（紧密型十进制）。[GDB]将为配置的目标使用适当的编码。


Because of a limitation in `libdecnumber` to manipulate decimal floating point numbers, it is not possible to convert (using a cast, for example) integers wider than 32-bit to decimal float.

> 由于`libdecnumber`在操作十进制浮点数方面的局限性，无法使用（例如，通过转换）将宽于32位的整数转换为十进制浮点数。


In addition, in order to imitate [GDB]'s behaviour with binary floating point computations, error checking in decimal float operations ignores underflow, overflow and divide by zero exceptions.

> 此外，为了模仿GDB在二进制浮点计算中的行为，十进制浮点操作中的错误检查忽略了溢出、下溢和除以零的异常。


In the PowerPC architecture, [GDB] provides a set of pseudo-registers to inspect `_Decimal128` values stored in floating point registers. See [PowerPC](PowerPC.html#PowerPC) for more details.

> 在PowerPC架构中，GDB提供了一组伪寄存器来检查存储在浮点寄存器中的_Decimal128值。有关更多详细信息，请参阅PowerPC。
