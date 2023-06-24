---
tip: translate by openai@2023-06-23 21:17:28
...
---
description: Fortran Operators (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Fortran Operators (Debugging with GDB)
lang: en
resource-type: document
title: Fortran Operators (Debugging with GDB)
---
::: header
Next: [Fortran Intrinsics](Fortran-Intrinsics.html#Fortran-Intrinsics)]
:::

---

#### 15.4.6.2 Fortran Operators and Expressions


Operators must be defined on values of specific types. For instance, `+` is defined on numbers, but not on characters or other non- arithmetic types. Operators are often defined on groups of types.

> 运算符必须在特定类型的值上定义。例如，“+”定义在数字上，而不是字符或其他非算术类型上。运算符通常定义在类型组上。

`**`


:   The exponentiation operator. It raises the first operand to the power of the second one.

> 运算符的乘方。它将第一个操作数提升到第二个操作数的幂。

`:`


:   The range operator. Normally used in the form of array(low:high) to represent a section of array.

> 范围运算符。通常以array(low:high)的形式使用，用来表示数组的一部分。

`%`


:   The access component operator. Normally used to access elements in derived types. Also suitable for unions. As unions aren't part of regular Fortran, this can only happen when accessing a register that uses a gdbarch-defined union type.

> 访问组件操作符。通常用于访问派生类型中的元素。也适用于联合。由于联合不是常规Fortran的一部分，因此只有在访问使用gdbarch定义的联合类型的寄存器时才会发生。

`::`


:   The scope operator. Normally used to access variables in modules or to set breakpoints on subroutines nested in modules or in other subroutines (internal subroutines).

> 范围操作符。通常用于访问模块中的变量，或在模块或其他子程序（内部子程序）中设置断点。
