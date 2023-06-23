---
description: M2 Operators (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: M2 Operators (Debugging with GDB)
lang: en
resource-type: document
title: M2 Operators (Debugging with GDB)
---
::: header
Next: [Built-In Func/Proc](Built_002dIn-Func_002fProc.html#Built_002dIn-Func_002fProc)]
:::

---

#### 15.4.9.1 Operators

Operators must be defined on values of specific types. For instance, `+` is defined on numbers, but not on structures. Operators are often defined on groups of types. For the purposes of Modula-2, the following definitions hold:

- *Integral types* consist of `INTEGER`, `CARDINAL`, and their subranges.
- *Character types* consist of `CHAR` and its subranges.
- *Floating-point types* consist of `REAL`.
- *Pointer types* consist of anything declared as `POINTER TO type`.
- *Scalar types* consist of all of the above.
- *Set types* consist of `SET` and `BITSET` types.
- *Boolean types* consist of `BOOLEAN`.

The following operators are supported, and appear in order of increasing precedence:

`,`

:   Function argument or array index separator.

`:=`

:   Assignment. The value of `var`.

`<, >`

:   Less than, greater than on integral, floating-point, or enumerated types.

`<=, >=`

:   Less than or equal to, greater than or equal to on integral, floating-point and enumerated types, or set inclusion on set types. Same precedence as `<`.

`=, <>, #`

:   Equality and two ways of expressing inequality, valid on scalar types. Same precedence as `<`. In [GDB] scripts, only `<>` is available for inequality, since `#` conflicts with the script comment character.

`IN`

:   Set membership. Defined on set types and the types of their members. Same precedence as `<`.

`OR`

:   Boolean disjunction. Defined on boolean types.

`AND, &`

:   Boolean conjunction. Defined on boolean types.

`@`

:   The [GDB] "artificial array" operator (see [Expressions](Expressions.html#Expressions)).

`+, -`

:   Addition and subtraction on integral and floating-point types, or union and difference on set types.

`*`

:   Multiplication on integral and floating-point types, or set intersection on set types.

`/`

:   Division on floating-point types, or symmetric set difference on set types. Same precedence as `*`.

`DIV, MOD`

:   Integer division and remainder. Defined on integral types. Same precedence as `*`.

`-`

:   Negative. Defined on `INTEGER` and `REAL` data.

`^`

:   Pointer dereferencing. Defined on pointer types.

`NOT`

:   Boolean negation. Defined on boolean types. Same precedence as `^`.

`.`

:   `RECORD` field selector. Defined on `RECORD` data. Same precedence as `^`.

``

:   Array indexing. Defined on `ARRAY` data. Same precedence as `^`.

`()`

:   Procedure argument list. Defined on `PROCEDURE` objects. Same precedence as `^`.

`::, .`

:   [GDB] and Modula-2 scope operators.

> *Warning:* Set expressions and their operations are not yet supported, so [GDB] treats the use of the operator `IN`, or the use of operators `+`, `-`, `*`, `/`, `=`, , `<>`, `#`, `<=`, and `>=` on sets as an error.

---

::: header
Next: [Built-In Func/Proc](Built_002dIn-Func_002fProc.html#Built_002dIn-Func_002fProc)]
:::
