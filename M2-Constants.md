---
tip: translate by openai@2023-06-23 23:58:16
...
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

> GDB允许您以以下方式表达Modula-2的常量：


- Integer constants are simply a sequence of digits. When used in an expression, a constant is interpreted to be type-compatible with the rest of the expression. Hexadecimal integers are specified by a trailing '`H`'.

> 整数常量只是一个数字序列。当在表达式中使用时，常量将被解释为与表达式其余部分兼容的类型。十六进制整数由后缀'H'指定。

- Floating point constants appear as a sequence of digits, followed by a decimal point and another sequence of digits. An optional exponent can then be specified, in the form '`E[+|-]nnn`' is the desired exponent. All of the digits of the floating point constant must be valid decimal (base 10) digits.

> 浮点常数以一串数字开头，后跟一个小数点和另一个数字序列。然后可以指定可选的指数，以'E[+|-]nnn'的形式指定。所有的浮点常数的数字必须是有效的十进制数（十进制）。

- Character constants consist of a single character enclosed by a pair of like quotes, either single (`'`) or double (`"`). They may also be expressed by their ordinal value (their [ASCII]'.

> 字符常量由一对相同的引号（单引号'或双引号"）中包含的单个字符组成。它们也可以用它们的序数值（它们的[ASCII]）表示。

- String constants consist of a sequence of characters enclosed by a pair of like quotes, either single (`'`) or double (`"`). Escape sequences in the style of C are also allowed. See [C and C++ Constants](C-Constants.html#C-Constants), for a brief explanation of escape sequences.

> 字符串常量由一对相同的引号（单引号`'`或双引号`"`）括起的字符序列组成。也允许使用C风格的转义序列。有关转义序列的简要解释，请参阅[C和C++常量](C-Constants.html#C-Constants)。
- Enumerated constants consist of an enumerated identifier.
- Boolean constants consist of the identifiers `TRUE` and `FALSE`.
- Pointer constants consist of integral values only.
- Set constants are not yet supported.
