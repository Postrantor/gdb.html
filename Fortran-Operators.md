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

`**`

:   The exponentiation operator. It raises the first operand to the power of the second one.

`:`

:   The range operator. Normally used in the form of array(low:high) to represent a section of array.

`%`

:   The access component operator. Normally used to access elements in derived types. Also suitable for unions. As unions aren't part of regular Fortran, this can only happen when accessing a register that uses a gdbarch-defined union type.

`::`

:   The scope operator. Normally used to access variables in modules or to set breakpoints on subroutines nested in modules or in other subroutines (internal subroutines).
