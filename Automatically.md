---
tip: translate by openai@2023-06-23 17:42:38
...
---
description: Automatically (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Automatically (Debugging with GDB)
lang: en
resource-type: document
title: Automatically (Debugging with GDB)
---
::: header
Previous: [Manually](Manually.html#Manually)]
:::

---

#### 15.1.3 Having [GDB]


To have [GDB] issues a warning.

> 要让GDB发出警告。


This may not seem necessary for most programs, which are written entirely in one source language. However, program modules and libraries written in one source language can be used by a main program written in a different source language. Using '`set language auto`' in this case frees you from having to set the working language manually.

> 对于完全用一种源语言编写的大多数程序来说，这可能不是必需的。但是，用一种源语言编写的程序模块和库可以被一个用不同源语言编写的主程序使用。在这种情况下，使用'`set language auto`'可以让您不必手动设置工作语言。
