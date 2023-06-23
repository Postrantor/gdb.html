---
description: M2 Constants (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: M2 Constants (Debugging with GDB)
lang: en
resource-type: document
title: M2 Constants (Debugging with GDB)
---
::: header
Next: [M2 Types](M2-Types.html#M2-Types)]
:::

---

#### 15.4.9.3 Constants

[GDB] allows you to express the constants of Modula-2 in the following ways:

- Integer constants are simply a sequence of digits. When used in an expression, a constant is interpreted to be type-compatible with the rest of the expression. Hexadecimal integers are specified by a trailing '`H`'.
- Floating point constants appear as a sequence of digits, followed by a decimal point and another sequence of digits. An optional exponent can then be specified, in the form '`E[+|-]nnn`' is the desired exponent. All of the digits of the floating point constant must be valid decimal (base 10) digits.
- Character constants consist of a single character enclosed by a pair of like quotes, either single (`'`) or double (`"`). They may also be expressed by their ordinal value (their [ASCII]'.
- String constants consist of a sequence of characters enclosed by a pair of like quotes, either single (`'`) or double (`"`). Escape sequences in the style of C are also allowed. See [C and C++ Constants](C-Constants.html#C-Constants), for a brief explanation of escape sequences.
- Enumerated constants consist of an enumerated identifier.
- Boolean constants consist of the identifiers `TRUE` and `FALSE`.
- Pointer constants consist of integral values only.
- Set constants are not yet supported.
