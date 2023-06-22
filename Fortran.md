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

Some Fortran compilers ([GNU] Fortran 77 and Fortran 95 compilers among them) append an underscore to the names of variables and functions. When you debug programs compiled by those compilers, you will need to refer to variables and functions with a trailing underscore.

Fortran symbols are usually case-insensitive, so [GDB]' command, see [Symbols](Symbols.html#Symbols), for the details.

---

• [Fortran Types](Fortran-Types.html#Fortran-Types):                                         Fortran builtin types
• [Fortran Operators](Fortran-Operators.html#Fortran-Operators):                             Fortran operators and expressions
• [Fortran Intrinsics](Fortran-Intrinsics.html#Fortran-Intrinsics):                          Fortran intrinsic functions
• [Special Fortran Commands](Special-Fortran-Commands.html#Special-Fortran-Commands) commands for Fortran

---
