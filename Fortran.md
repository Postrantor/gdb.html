---
tip: translate by openai@2023-06-23 21:18:44
...
---
description: Fortran (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Fortran (Debugging with GDB)
lang: en
resource-type: document
title: Fortran (Debugging with GDB)
---
::: header
Next: [Pascal](Pascal.html#Pascal)]
:::

---

#### 15.4.6 Fortran


[GDB] can be used to debug programs written in Fortran. Note, that not all Fortran language features are available yet.

> GDB可以用来调试用Fortran编写的程序。注意，尚不支持所有的Fortran语言特性。


Some Fortran compilers ([GNU] Fortran 77 and Fortran 95 compilers among them) append an underscore to the names of variables and functions. When you debug programs compiled by those compilers, you will need to refer to variables and functions with a trailing underscore.

> 一些Fortran编译器（其中包括[GNU] Fortran 77和Fortran 95编译器）会在变量和函数名称后面添加下划线。在调试这些编译器编译的程序时，您将需要使用带有尾部下划线的变量和函数进行引用。


Fortran symbols are usually case-insensitive, so [GDB]' command, see [Symbols](Symbols.html#Symbols), for the details.

> 符号在Fortran中通常不区分大小写，所以[GDB]命令可参考[符号](Symbols.html#Symbols)，查看详细信息。

---


• [Fortran Types](Fortran-Types.html#Fortran-Types):                                         Fortran builtin types

> • [Fortran 类型](Fortran-Types.html#Fortran-Types)：Fortran 内置类型

• [Fortran Operators](Fortran-Operators.html#Fortran-Operators):                             Fortran operators and expressions

> • [Fortran 操作符](Fortran-Operators.html#Fortran-Operators):                             Fortran 操作符和表达式

• [Fortran Intrinsics](Fortran-Intrinsics.html#Fortran-Intrinsics):                          Fortran intrinsic functions

> • [Fortran 内置函数](Fortran-Intrinsics.html#Fortran-Intrinsics):                           Fortran 内置函数

• [Special Fortran Commands](Special-Fortran-Commands.html#Special-Fortran-Commands) commands for Fortran

> • [特殊Fortran命令](Special-Fortran-Commands.html#Special-Fortran-Commands) 用于Fortran的命令

---
