---
description: Fortran Types (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Fortran Types (Debugging with GDB)
lang: en
resource-type: document
title: Fortran Types (Debugging with GDB)
---
::: header
Next: [Fortran Operators](Fortran-Operators.html#Fortran-Operators)]
:::

---

#### 15.4.6.1 Fortran Types

In Fortran the primitive data-types have an associated `KIND` type parameter, written as '`type*kindparam`'. The kind of a type can be retrieved by using the intrinsic function `KIND`, see [Fortran Intrinsics](Fortran-Intrinsics.html#Fortran-Intrinsics).

Generally, the actual implementation of the `KIND` type parameter is compiler specific. In [GDB] specifies its size in memory --- a Fortran `Integer*4` or `Integer(kind=4)` would be an integer type occupying 4 bytes of memory. An exception to this rule is the `Complex` type for which the kind of the type does not specify its entire size, but the size of each of the two `Real`'s it is composed of. A `Complex*4` would thus consist of two `Real*4` s and occupy 8 bytes of memory.

For every type there is also a default kind associated with it, e.g. `Integer` in [GDB].

Not every kind parameter is valid for every type and in [GDB] the following type kinds are available.

`Integer`

:   `Integer*1`, `Integer*2`, `Integer*4`, `Integer*8`, and `Integer` = `Integer*4`.

`Logical`

:   `Logical*1`, `Logical*2`, `Logical*4`, `Logical*8`, and `Logical` = `Logical*4`.

`Real`

:   `Real*4`, `Real*8`, `Real*16`, and `Real` = `Real*4`.

`Complex`

:   `Complex*4`, `Complex*8`, `Complex*16`, and `Complex` = `Complex*4`.

---

::: header
Next: [Fortran Operators](Fortran-Operators.html#Fortran-Operators)]
:::
