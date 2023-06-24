---
tip: translate by openai@2023-06-23 23:46:45
...
---
description: Languages (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Languages (Debugging with GDB)
lang: en
resource-type: document
title: Languages (Debugging with GDB)
---
::: header
Next: [Symbols](Symbols.html#Symbols)]
:::

---

## 15 Using [GDB]


Although programming languages generally have common aspects, they are rarely expressed in the same manner. For instance, in ANSI C, dereferencing a pointer `p` is accomplished by `*p`, but in Modula-2, it is accomplished by `p^`. Values can also be represented (and displayed) differently. Hex numbers in C appear as '`0x1ae`'.

> 尽管编程语言通常有共同的方面，但它们很少以相同的方式表达。例如，在ANSI C中，通过`*p`解引用指针`p`，而在Modula-2中，则通过`p^`来实现。值也可以以不同的方式表示（并显示）。C中的十六进制数字出现为`0x1ae`。


Language-specific information is built into [GDB] to output values in a manner consistent with the syntax of your program's native language. The language you use to build expressions is called the *working language*.

> GDB内置了语言特定的信息，以便以与您的程序本地语言的语法一致的方式输出值。用于构建表达式的语言称为*工作语言*。

---


• [Setting](Setting.html#Setting):                                                  Switching between source languages

> • [设置](Setting.html#Setting)：切换源语言

• [Show](Show.html#Show):                                                           Displaying the language

> • [显示](Show.html#Show): 显示语言

• [Checks](Checks.html#Checks):                                                     Type and range checks

> • 检查（Checks.html#Checks）：类型和范围检查

• [Supported Languages](Supported-Languages.html#Supported-Languages):              Supported languages

> • [支持的语言](Supported-Languages.html#Supported-Languages)：支持的语言

• [Unsupported Languages](Unsupported-Languages.html#Unsupported-Languages):        Unsupported languages

> • [不支持的语言](Unsupported-Languages.html#Unsupported-Languages):        不支持的语言

---
