---
tip: translate by openai@2023-06-24 03:24:41
...
---
description: Summary (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Summary (Debugging with GDB)
lang: en
resource-type: document
title: Summary (Debugging with GDB)
---
::: header
Next: [Sample Session](Sample-Session.html#Sample-Session)]
:::

---

## Summary of [GDB]


The purpose of a debugger such as [GDB] is to allow you to see what is going on "inside" another program while it executes---or what another program was doing at the moment it crashed.

> 调试器（如GDB）的目的是在另一个程序执行时让你看到它内部发生的情况---或者它在崩溃时正在做什么。


[GDB] can do four main kinds of things (plus other things in support of these) to help you catch bugs in the act:

> [GDB] 可以做四种主要的事情（以及其他支持这些的事情）来帮助你抓住缺陷：

- Start your program, specifying anything that might affect its behavior.
- Make your program stop on specified conditions.
- Examine what has happened, when your program has stopped.

- Change things in your program, so you can experiment with correcting the effects of one bug and go on to learn about another.

> 改变你的程序中的事情，这样你就可以尝试纠正一个错误的影响，然后继续学习另一个错误。


You can use [GDB] to debug programs written in C and C++. For more information, see [Supported Languages](Supported-Languages.html#Supported-Languages). For more information, see [C and C++](C.html#C).

> 你可以使用GDB来调试用C和C++编写的程序。更多信息，请参见[支持的语言](Supported-Languages.html#Supported-Languages)。更多信息，请参见[C和C++](C.html#C)。

Support for D is partial. For information on D, see [D](D.html#D).


Support for Modula-2 is partial. For information on Modula-2, see [Modula-2](Modula_002d2.html#Modula_002d2).

> 对 Modula-2 的支持是部分的。有关 Modula-2 的信息，请参阅[Modula-2](Modula_002d2.html#Modula_002d2)。


Support for OpenCL C is partial. For information on OpenCL C, see [OpenCL C](OpenCL-C.html#OpenCL-C).

> 对OpenCL C的支持是部分的。有关OpenCL C的信息，请参阅[OpenCL C](OpenCL-C.html#OpenCL-C)。


Debugging Pascal programs which use sets, subranges, file variables, or nested functions does not currently work. [GDB] does not support entering expressions, printing values, or similar features using Pascal syntax.

> 调试使用集合、子范围、文件变量或嵌套函数的Pascal程序目前不能工作。[GDB]不支持使用Pascal语法输入表达式、打印值或类似功能。


[GDB] can be used to debug programs written in Fortran, although it may be necessary to refer to some variables with a trailing underscore.

> GDB 可用于调试用Fortran编写的程序，尽管有时可能需要以尾部带下划线的形式引用某些变量。


[GDB] can be used to debug programs written in Objective-C, using either the Apple/NeXT or the GNU Objective-C runtime.

> GDB可以用来调试用Apple/NeXT或GNU Objective-C运行时编写的程序。

---


• [Free Software](Free-Software.html#Free-Software):                       Freely redistributable software

> • [自由软件](Free-Software.html#Free-Software):                可自由再发行的软件

• [Free Documentation](Free-Documentation.html#Free-Documentation):        Free Software Needs Free Documentation

> • [免费文档](Free-Documentation.html#Free-Documentation):        免费软件需要免费文档

• [Contributors](Contributors.html#Contributors):                          Contributors to GDB

> • [贡献者](Contributors.html#Contributors): 贡献GDB的人

---

---

::: header
Next: [Sample Session](Sample-Session.html#Sample-Session)]
:::
