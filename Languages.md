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

Language-specific information is built into [GDB] to output values in a manner consistent with the syntax of your program's native language. The language you use to build expressions is called the *working language*.

---

• [Setting](Setting.html#Setting):                                                  Switching between source languages
• [Show](Show.html#Show):                                                           Displaying the language
• [Checks](Checks.html#Checks):                                                     Type and range checks
• [Supported Languages](Supported-Languages.html#Supported-Languages):              Supported languages
• [Unsupported Languages](Unsupported-Languages.html#Unsupported-Languages):        Unsupported languages

---
