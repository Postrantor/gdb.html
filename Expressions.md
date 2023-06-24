---
tip: translate by openai@2023-06-23 20:59:01
...
---
description: Expressions (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Expressions (Debugging with GDB)
lang: en
resource-type: document
title: Expressions (Debugging with GDB)
---
::: header
Next: [Ambiguous Expressions](Ambiguous-Expressions.html#Ambiguous-Expressions)]
:::

---

### 10.1 Expressions

`print` and many other [GDB]. This includes conditional expressions, function calls, casts, and string constants. It also includes preprocessor macros, if you compiled your program to include this information; see [Compilation](Compilation.html#Compilation).


[GDB] copies the array to memory that is `malloc` ed in the target program.

> GDB 将数组复制到在目标程序中用 `malloc` 分配的内存中。


Because C is so widespread, most of the expressions shown in examples in this manual are in C. See [Using [GDB] with Different Languages](Languages.html#Languages), for information on how to use expressions in other languages.

> 因为C语言广泛使用，本手册中的示例表达式大多是C语言。有关如何使用其他语言的表达式的信息，请参阅[使用[GDB]与不同语言](Languages.html#Languages)。


In this section, we discuss operators that you can use in [GDB] expressions regardless of your programming language.

> 在本节中，我们讨论了您可以在[GDB]表达式中使用的操作符，而无需考虑您的编程语言。


Casts are supported in all languages, not just in C, because it is so useful to cast a number into a pointer in order to examine a structure at that address in memory.

> 所有语言都支持转换，而不仅仅是C，因为将一个数字转换为指针，以便检查内存中该地址的结构是非常有用的。


[GDB] supports these operators, in addition to those common to programming languages:

> [GDB]除了支持编程语言中的常见运算符外，还支持以下运算符。

`@`


:   '`@`' is a binary operator for treating parts of memory as arrays. See [Artificial Arrays](Arrays.html#Arrays), for more information.

> '@'是一个二进制运算符，用于将内存的部分作为数组来处理。有关更多信息，请参阅[人工数组](Arrays.html#Arrays)。

`::`


:   '`::`' allows you to specify a variable in terms of the file or function where it is defined. See [Program Variables](Variables.html#Variables).

> `::`允许您以定义该变量的文件或函数的方式指定变量。请参阅[程序变量](Variables.html#Variables)。

```

```

` addr`

:   Refers to an object of type `type`.

---

::: header
Next: [Ambiguous Expressions](Ambiguous-Expressions.html#Ambiguous-Expressions)]
:::
