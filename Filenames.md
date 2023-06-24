---
tip: translate by openai@2023-06-23 21:01:44
...
---
description: Filenames (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Filenames (Debugging with GDB)
lang: en
resource-type: document
title: Filenames (Debugging with GDB)
---
::: header
Next: [Manually](Manually.html#Manually)]
:::

---

#### 15.1.1 List of Filename Extensions and Languages


If a source file name ends in one of the following extensions, then [GDB] infers that its language is the one indicated.

> 如果源文件名以下列扩展名结尾，那么[GDB]推断其语言为指定的语言。

`.ada`
`.ads`
`.adb`
`.a`

:   Ada source file.

`.c`

:   C source file

`.C`
`.cc`
`.cp`
`.cpp`
`.cxx`
`.c++`

:   C++ source file

`.d`

:   D source file

`.m`

:   Objective-C source file

`.f`
`.F`

:   Fortran source file

`.mod`

:   Modula-2 source file

`.s`
`.S`


:   Assembler source file. This actually behaves almost like C, but [GDB] does not skip over function prologues when stepping.

> 组装器源文件。它实际上的行为几乎和C一样，但[GDB]在调试时不会跳过函数的开头部分。


In addition, you may set the language associated with a filename extension. See [Displaying the Language](Show.html#Show).

> 此外，您可以设置与文件扩展名关联的语言。请参见[显示语言](Show.html#Show)。
