---
tip: translate by openai@2023-06-23 18:41:32
...
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

> GDB允许您以下列方式表达C和C++的常量：


- Integer constants are a sequence of digits. Octal constants are specified by a leading '`0`', specifying that the constant should be treated as a `long` value.

> 整数常量是一个数字序列。八进制常量由前导'0'指定，表示常量应被视为长整型值。

- Floating point constants are a sequence of digits, followed by a decimal point, followed by a sequence of digits, and optionally followed by an exponent. An exponent is of the form: '`e[[+]|-]nnn`', which specifies a `long double` constant.

> 浮点常量是一串数字，后面跟着一个小数点，然后是一串数字，可选择性地后面跟着指数。指数的形式是：'e[[+]|-]nnn'，它指定一个长双精度常量。
- Enumerated constants consist of enumerated identifiers, or their integral equivalents.

- Character constants are a single character surrounded by single quotes (`'`), or a number---the ordinal value of the corresponding character (usually its [ASCII]' for newline.

> 字符常量是用单引号（'）括起来的单个字符，或者一个数字——对应字符的序数值（通常是其[ASCII]的），用于换行。


  Wide character constants can be written by prefixing a character constant with '`L`'. The target wide character set is used when computing the value of this constant (see [Character Sets](Character-Sets.html#Character-Sets)).

> 宽字符常量可以通过在字符常量前加上'L'来书写。计算这个常量的值时会使用目标宽字符集（请参见[字符集](Character-Sets.html#Character-Sets)）。

- String constants are a sequence of character constants surrounded by double quotes (`"`). Any valid character constant (as described above) may appear. Double quotes within the string must be preceded by a backslash, so for instance '`"a\"b'c"`' is a string of five characters.

> 字符串常量是由双引号（`"`）括起来的字符常量序列。可以出现任何有效的字符常量（如上所述）。字符串中的双引号必须被反斜杠所引导，因此例如'`"a\"b'c"`'就是一个由五个字符组成的字符串。


  Wide string constants can be written by prefixing a string constant with '`L`', as in C. The target wide character set is used when computing the value of this constant (see [Character Sets](Character-Sets.html#Character-Sets)).

> 宽字符串常量可以通过用' L'前缀来写，就像C语言一样。计算此常量的值时使用目标宽字符集（参见[字符集]（Character-Sets.html#Character-Sets））。

- Pointer constants are an integral value. You can also write pointers to constants using the C operator '`&`'.

> 指针常量是一个整数值。您也可以使用C运算符'&'来编写指向常量的指针。

- Array constants are comma-separated lists surrounded by braces '`' is a three-element array of pointers.

> 数组常量是用大括号括起来的逗号分隔的列表。这是一个由三个指针组成的数组。

---

::: header
Next: [C Plus Plus Expressions](C-Plus-Plus-Expressions.html#C-Plus-Plus-Expressions)]
:::
