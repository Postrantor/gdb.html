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

Because C is so widespread, most of the expressions shown in examples in this manual are in C. See [Using [GDB] with Different Languages](Languages.html#Languages), for information on how to use expressions in other languages.

In this section, we discuss operators that you can use in [GDB] expressions regardless of your programming language.

Casts are supported in all languages, not just in C, because it is so useful to cast a number into a pointer in order to examine a structure at that address in memory.

[GDB] supports these operators, in addition to those common to programming languages:

`@`

:   '`@`' is a binary operator for treating parts of memory as arrays. See [Artificial Arrays](Arrays.html#Arrays), for more information.

`::`

:   '`::`' allows you to specify a variable in terms of the file or function where it is defined. See [Program Variables](Variables.html#Variables).

```

```

` addr`

:   Refers to an object of type `type`.

---

::: header
Next: [Ambiguous Expressions](Ambiguous-Expressions.html#Ambiguous-Expressions)]
:::
