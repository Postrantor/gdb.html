---
tip: translate by openai@2023-06-24 01:52:05
...
---
description: Readline Arguments (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Readline Arguments (Debugging with GDB)
lang: en
resource-type: document
title: Readline Arguments (Debugging with GDB)
---
::: header
Next: [Searching](Searching.html#Searching)]
:::

---

#### 33.2.4 Readline Arguments


You can pass numeric arguments to Readline commands. Sometimes the argument acts as a repeat count, other times it is the *sign* of the argument that is significant. If you pass a negative argument to a command which normally acts in a forward direction, that command will act in a backward direction. For example, to kill text back to the start of the line, you might type '`M-- C-k`'.

> 你可以向Readline命令传递数字参数。有时参数充当重复计数，有时参数的*符号*才是重要的。如果向通常向前执行的命令传递负参数，该命令将向后执行。例如，要将文本清除到行首，您可以键入“ M-- C-k”。


The general way to pass numeric arguments to a command is to type meta digits before the command. If the first 'digit' typed is a minus sign ('`-`', which will delete the next ten characters on the input line.

> 一般的方法是在命令前输入元数字来传递数字参数。如果第一个输入的数字是减号（'-'），将会删除输入行上的下十个字符。
