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

There are two encodings in use, depending on the architecture: BID (Binary Integer Decimal) for x86 and x86-64, and DPD (Densely Packed Decimal) for PowerPC and S/390. [GDB] will use the appropriate encoding for the configured target.

Because of a limitation in `libdecnumber` to manipulate decimal floating point numbers, it is not possible to convert (using a cast, for example) integers wider than 32-bit to decimal float.

In addition, in order to imitate [GDB]'s behaviour with binary floating point computations, error checking in decimal float operations ignores underflow, overflow and divide by zero exceptions.

In the PowerPC architecture, [GDB] provides a set of pseudo-registers to inspect `_Decimal128` values stored in floating point registers. See [PowerPC](PowerPC.html#PowerPC) for more details.
