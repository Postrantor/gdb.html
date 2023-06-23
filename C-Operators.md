---
description: C Operators (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: C Operators (Debugging with GDB)
lang: en
resource-type: document
title: C Operators (Debugging with GDB)
---
::: header
Next: [C Constants](C-Constants.html#C-Constants)]
:::

---

#### 15.4.1.1 C and C++ Operators

Operators must be defined on values of specific types. For instance, `+` is defined on numbers, but not on structures. Operators are often defined on groups of types.

For the purposes of C and C++, the following definitions hold:

- *Integral types* include `int` with any of its storage-class specifiers; `char`; `enum`; and, for C++, `bool`.
- *Floating-point types* include `float`, `double`, and `long double` (if supported by the target platform).
- *Pointer types* include all types defined as `(type *)`.
- *Scalar types* include all of the above.

The following operators are supported. They are listed here in order of increasing precedence:

`,`

:   The comma or sequencing operator. Expressions in a comma-separated list are evaluated from left to right, with the result of the entire expression being the last expression evaluated.

`=`

:   Assignment. The value of an assignment expression is the value assigned. Defined on scalar types.

`op=`

:   Used in an expression of the form `a op= b`, and translated to `a = a op b`. `op=` and `=` have the same precedence. The operator `op` is any one of the operators `|`, `^`, `&`, `<<`, `>>`, `+`, `-`, `*`, `/`, `%`.

`?:`

:   The ternary operator. `a ? b : c` can be thought of as: if `a` should be of an integral type.

`||`

:   Logical [OR]. Defined on integral types.

`&&`

:   Logical [AND]. Defined on integral types.

`|`

:   Bitwise [OR]. Defined on integral types.

`^`

:   Bitwise exclusive-[OR]. Defined on integral types.

`&`

:   Bitwise [AND]. Defined on integral types.

`==, !=`

:   Equality and inequality. Defined on scalar types. The value of these expressions is 0 for false and non-zero for true.

`<, >, <=, >=`

:   Less than, greater than, less than or equal, greater than or equal. Defined on scalar types. The value of these expressions is 0 for false and non-zero for true.

`<<, >>`

:   left shift, and right shift. Defined on integral types.

`@`

:   The [GDB] "artificial array" operator (see [Expressions](Expressions.html#Expressions)).

`+, -`

:   Addition and subtraction. Defined on integral types, floating-point types and pointer types.

`*, /, %`

:   Multiplication, division, and modulus. Multiplication and division are defined on integral and floating-point types. Modulus is defined on integral types.

`++, --`

:   Increment and decrement. When appearing before a variable, the operation is performed before the variable is used in an expression; when appearing after it, the variable's value is used before the operation takes place.

`*`

:   Pointer dereferencing. Defined on pointer types. Same precedence as `++`.

`&`

:   Address operator. Defined on variables. Same precedence as `++`.

```
For debugging C++, [GDB]') is stored.
```

`-`

:   Negative. Defined on integral and floating-point types. Same precedence as `++`.

`!`

:   Logical negation. Defined on integral types. Same precedence as `++`.

`~`

:   Bitwise complement operator. Defined on integral types. Same precedence as `++`.

`., ->`

:   Structure member, and pointer-to-structure member. For convenience, [GDB] regards the two as equivalent, choosing whether to dereference a pointer based on the stored type information. Defined on `struct` and `union` data.

`.*, ->*`

:   Dereferences of pointers to members.

``

:   Array indexing. `a[i]` is defined as `*(a+i)`. Same precedence as `->`.

`()`

:   Function parameter list. Same precedence as `->`.

`::`

:   C++ scope resolution operator. Defined on `struct`, `union`, and `class` types.

`::`

:   Doubled colons also represent the [GDB] scope operator (see [Expressions](Expressions.html#Expressions)). Same precedence as `::`, above.

If an operator is redefined in the user code, [GDB] usually attempts to invoke the redefined version instead of using the operator's predefined meaning.

---

::: header
Next: [C Constants](C-Constants.html#C-Constants)]
:::
