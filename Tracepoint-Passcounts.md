---
tip: translate by openai@2023-06-23 14:48:01
...
---
description: Tracepoint Passcounts (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Tracepoint Passcounts (Debugging with GDB)
lang: en
resource-type: document
title: Tracepoint Passcounts (Debugging with GDB)
-------------------------------------------------

::: header
Next: [Tracepoint Conditions](Tracepoint-Conditions.html#Tracepoint-Conditions)]
:::

---

#### 13.1.3 Tracepoint Passcounts

`passcount [n [num]]`

Set the *passcount* of a tracepoint. The passcount is a way to automatically stop a trace experiment. If a tracepoint's passcount is `n` is not specified, the `passcount` command sets the passcount of the most recently defined tracepoint. If no passcount is given, the trace experiment will run until stopped explicitly by the user.

> 设置断点的通过计数。通过计数是一种自动停止跟踪实验的方式。如果断点的通过计数未指定，则“passcount”命令将设置最近定义的断点的通过计数。如果没有给出通过计数，跟踪实验将一直运行，直到用户明确停止。

Examples:

::: smallexample

```bash
(gdb) passcount 5 2 // Stop on the 5th execution of
```

```bash
                                   // tracepoint 2
```

```bash
(gdb) passcount 12  // Stop on the 12th execution of the
```

```bash
                                   // most recently defined tracepoint.
```

```bash
(gdb) trace foo
(gdb) pass 3
(gdb) trace bar
(gdb) pass 2
(gdb) trace baz
(gdb) pass 1        // Stop tracing when foo has been
```

```bash
                                    // executed 3 times OR when bar has
```

```bash
                                    // been executed 2 times
```

```bash
                                    // OR when baz has been executed 1 time.
```

:::
