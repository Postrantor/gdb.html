---
tip: translate by openai@2023-06-23 18:56:01
...
---
description: Checks (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Checks (Debugging with GDB)
lang: en
resource-type: document
title: Checks (Debugging with GDB)
---
::: header
Next: [Supported Languages](Supported-Languages.html#Supported-Languages)]
:::

---

### 15.3 Type and Range Checking


Some languages are designed to guard you against making seemingly common errors through a series of compile- and run-time checks. These include checking the type of arguments to functions and operators and making sure mathematical overflows are caught at run time. Checks such as these help to ensure a program's correctness once it has been compiled by eliminating type mismatches and providing active checks for range errors when your program is running.

> 一些语言旨在通过一系列编译时和运行时检查来防止您犯常见错误。这些包括检查函数和操作符的参数类型以及确保在运行时捕获数学溢出。这些检查有助于在编译程序后确保程序的正确性，通过消除类型不匹配并在程序运行时提供范围错误的主动检查。


By default [GDB] for evaluation via the `print` command, for example.

> 默认情况下，GDB可以通过`print`命令来进行评估，例如。

---


• [Type Checking](Type-Checking.html#Type-Checking):           An overview of type checking

> •[类型检查](Type-Checking.html#Type-Checking):           类型检查概述

• [Range Checking](Range-Checking.html#Range-Checking):        An overview of range checking

> • [范围检查](Range-Checking.html#Range-Checking): 一个范围检查的概述

---
