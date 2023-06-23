---
description: Built-In Func/Proc (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Built-In Func/Proc (Debugging with GDB)
lang: en
resource-type: document
title: Built-In Func/Proc (Debugging with GDB)
---
::: header
Next: [M2 Constants](M2-Constants.html#M2-Constants)]
:::

---

#### 15.4.9.2 Built-in Functions and Procedures

Modula-2 also makes available several built-in procedures and functions. In describing these, the following metavariables are used:

`a`

:   represents an `ARRAY` variable.

`c`

:   represents a `CHAR` constant or variable.

`i`

:   represents a variable or constant of integral type.

`m`

:   represents an identifier that belongs to a set. Generally used in the same function with the metavariable `s`).

`n`

:   represents a variable or constant of integral or floating-point type.

`r`

:   represents a variable or constant of floating-point type.

`t`

:   represents a type.

`v`

:   represents a variable.

`x`

:   represents a variable or constant of one of many types. See the explanation of the function for details.

All Modula-2 built-in procedures also return a result, described below.

`ABS(n)`

:   Returns the absolute value of `n`.

`CAP(c)`

:   If `c` is a lower case letter, it returns its upper case equivalent, otherwise it returns its argument.

`CHR(i)`

:   Returns the character whose ordinal value is `i`.

`DEC(v)`

:   Decrements the value in the variable `v` by one. Returns the new value.

`DEC(v,i)`

:   Decrements the value in the variable `v`. Returns the new value.

`EXCL(m,s)`

:   Removes the element `m`. Returns the new set.

`FLOAT(i)`

:   Returns the floating point equivalent of the integer `i`.

`HIGH(a)`

:   Returns the index of the last member of `a`.

`INC(v)`

:   Increments the value in the variable `v` by one. Returns the new value.

`INC(v,i)`

:   Increments the value in the variable `v`. Returns the new value.

`INCL(m,s)`

:   Adds the element `m` if it is not already there. Returns the new set.

`MAX(t)`

:   Returns the maximum value of the type `t`.

`MIN(t)`

:   Returns the minimum value of the type `t`.

`ODD(i)`

:   Returns boolean TRUE if `i` is an odd number.

`ORD(x)`

:   Returns the ordinal value of its argument. For example, the ordinal value of a character is its [ASCII] must be of an ordered type, which include integral, character and enumerated types.

`SIZE(x)`

:   Returns the size of its argument. The argument `x` can be a variable or a type.

`TRUNC(r)`

:   Returns the integral part of `r`.

`TSIZE(x)`

:   Returns the size of its argument. The argument `x` can be a variable or a type.

`VAL(t,i)`

:   Returns the member of the type `t`.

> *Warning:* Sets and their operations are not yet supported, so [GDB] treats the use of procedures `INCL` and `EXCL` as an error.

---

::: header
Next: [M2 Constants](M2-Constants.html#M2-Constants)]
:::
