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

In addition, you may set the language associated with a filename extension. See [Displaying the Language](Show.html#Show).
