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

Tracepoint conditions can be specified when a tracepoint is set, by using '`if`' in the arguments to the `trace` command. See [Setting Tracepoints](Create-and-Delete-Tracepoints.html#Create-and-Delete-Tracepoints). They can also be set or changed at any time with the `condition` command, just as with breakpoints.

Unlike breakpoint conditions, [GDB]. Global variables become raw memory locations, locals become stack accesses, and so forth.

For instance, suppose you have a function that is usually called frequently, but should not be called after an error has occurred. You could use the following tracepoint command to collect data about calls of that function that happen while the error code is propagating through the program; an unconditional tracepoint could end up collecting thousands of useless trace frames that you would have to search through.

::: smallexample

```bash
(gdb) trace normal_operation if errcode > 0
```

:::
