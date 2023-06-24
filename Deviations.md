---
tip: translate by openai@2023-06-23 20:31:42
...
---
description: Deviations (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Deviations (Debugging with GDB)
lang: en
resource-type: document
title: Deviations (Debugging with GDB)
---
::: header
Next: [M2 Checks](M2-Checks.html#M2-Checks)]
:::

---

#### 15.4.9.6 Deviations from Standard Modula-2


A few changes have been made to make Modula-2 programs easier to debug. This is done primarily via loosening its type strictness:

> 为了使Modula-2程序更容易调试，已经做出了一些改变。这主要是通过放宽类型严格性来实现的：


- Unlike in standard Modula-2, pointer constants can be formed by integers. This allows you to modify pointer variables during debugging. (In standard Modula-2, the actual address contained in a pointer variable is hidden from you; it can only be modified through direct assignment to another pointer variable or expression that returned a pointer.)

> 在标准Modula-2中不同，可以用整数来形成指针常量。这使您可以在调试期间修改指针变量。（在标准Modula-2中，指针变量中包含的实际地址对您是隐藏的；它只能通过直接赋值给另一个指针变量或返回指针的表达式来修改。）

- C escape sequences can be used in strings and characters to represent non-printable characters. [GDB]' format.

> C 逃逸序列可以用于字符串和字符中来表示不可打印的字符（GDB）。
- The assignment operator (`:=`) returns the value of its right-hand argument.
- All built-in procedures both modify *and* return their argument.
