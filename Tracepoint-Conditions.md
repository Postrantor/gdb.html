---
tip: translate by openai@2023-06-23 14:45:12
...
---
description: Tracepoint Conditions (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Tracepoint Conditions (Debugging with GDB)
lang: en
resource-type: document
title: Tracepoint Conditions (Debugging with GDB)
---
::: header
Next: [Trace State Variables](Trace-State-Variables.html#Trace-State-Variables)]
:::

---

#### 13.1.4 Tracepoint Conditions


The simplest sort of tracepoint collects data every time your program reaches a specified place. You can also specify a *condition* for a tracepoint. A condition is just a Boolean expression in your programming language (see [Expressions](Expressions.html#Expressions)). A tracepoint with a condition evaluates the expression each time your program reaches it, and data collection happens only if the condition is true.

> 最简单的跟踪点每次程序到达指定位置时就会收集数据。您还可以为跟踪点指定*条件*。条件只是编程语言中的布尔表达式（参见[表达式](Expressions.html#Expressions)）。具有条件的跟踪点每次程序到达时都会评估表达式，只有当条件为真时才会发生数据收集。


Tracepoint conditions can be specified when a tracepoint is set, by using '`if`' in the arguments to the `trace` command. See [Setting Tracepoints](Create-and-Delete-Tracepoints.html#Create-and-Delete-Tracepoints). They can also be set or changed at any time with the `condition` command, just as with breakpoints.

> 可以通过在`trace`命令的参数中使用`if`来指定跟踪点条件。参见[设置跟踪点](Create-and-Delete-Tracepoints.html#Create-and-Delete-Tracepoints)。它们也可以随时使用`condition`命令设置或更改，就像断点一样。


Unlike breakpoint conditions, [GDB]. Global variables become raw memory locations, locals become stack accesses, and so forth.

> 与断点条件不同，[GDB]。全局变量变成原始内存位置，本地变量变成堆栈访问，等等。


For instance, suppose you have a function that is usually called frequently, but should not be called after an error has occurred. You could use the following tracepoint command to collect data about calls of that function that happen while the error code is propagating through the program; an unconditional tracepoint could end up collecting thousands of useless trace frames that you would have to search through.

> 例如，假设您有一个通常经常被调用的函数，但在发生错误后不应该调用。您可以使用以下tracepoint命令来收集期间发生错误代码传播到程序中的该函数调用的数据; 无条件的tracepoint可能会收集数以千计的无用的跟踪帧，您必须搜索。

::: smallexample

```bash
(gdb) trace normal_operation if errcode > 0
```

:::
