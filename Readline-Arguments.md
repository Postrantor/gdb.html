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

The general way to pass numeric arguments to a command is to type meta digits before the command. If the first 'digit' typed is a minus sign ('`-`', which will delete the next ten characters on the input line.
