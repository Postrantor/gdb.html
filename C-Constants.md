---
description: C Constants (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: C Constants (Debugging with GDB)
lang: en
resource-type: document
title: C Constants (Debugging with GDB)
---
::: header
Next: [C Plus Plus Expressions](C-Plus-Plus-Expressions.html#C-Plus-Plus-Expressions)]
:::

---

#### 15.4.1.2 C and C++ Constants

[GDB] allows you to express the constants of C and C++ in the following ways:

- Integer constants are a sequence of digits. Octal constants are specified by a leading '`0`', specifying that the constant should be treated as a `long` value.
- Floating point constants are a sequence of digits, followed by a decimal point, followed by a sequence of digits, and optionally followed by an exponent. An exponent is of the form: '`e[[+]|-]nnn`', which specifies a `long double` constant.
- Enumerated constants consist of enumerated identifiers, or their integral equivalents.
- Character constants are a single character surrounded by single quotes (`'`), or a number---the ordinal value of the corresponding character (usually its [ASCII]' for newline.

  Wide character constants can be written by prefixing a character constant with '`L`'. The target wide character set is used when computing the value of this constant (see [Character Sets](Character-Sets.html#Character-Sets)).
- String constants are a sequence of character constants surrounded by double quotes (`"`). Any valid character constant (as described above) may appear. Double quotes within the string must be preceded by a backslash, so for instance '`"a\"b'c"`' is a string of five characters.

  Wide string constants can be written by prefixing a string constant with '`L`', as in C. The target wide character set is used when computing the value of this constant (see [Character Sets](Character-Sets.html#Character-Sets)).
- Pointer constants are an integral value. You can also write pointers to constants using the C operator '`&`'.
- Array constants are comma-separated lists surrounded by braces '`' is a three-element array of pointers.

---

::: header
Next: [C Plus Plus Expressions](C-Plus-Plus-Expressions.html#C-Plus-Plus-Expressions)]
:::
