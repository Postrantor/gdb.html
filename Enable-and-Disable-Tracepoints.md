---
description: Enable and Disable Tracepoints (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Enable and Disable Tracepoints (Debugging with GDB)
lang: en
resource-type: document
title: Enable and Disable Tracepoints (Debugging with GDB)
---
::: header
Next: [Tracepoint Passcounts](Tracepoint-Passcounts.html#Tracepoint-Passcounts)]
:::

---

#### 13.1.2 Enable and Disable Tracepoints

These commands are deprecated; they are equivalent to plain `disable` and `enable`.

`disable tracepoint [num]`

Disable tracepoint `num` is given. A disabled tracepoint will have no effect during a trace experiment, but it is not forgotten. You can re-enable a disabled tracepoint using the `enable tracepoint` command. If the command is issued during a trace experiment and the debug target has support for disabling tracepoints during a trace experiment, then the change will be effective immediately. Otherwise, it will be applied to the next trace experiment.

`enable tracepoint [num]`

Enable tracepoint `num`, or all tracepoints. If this command is issued during a trace experiment and the debug target supports enabling tracepoints during a trace experiment, then the enabled tracepoints will become effective immediately. Otherwise, they will become effective the next time a trace experiment is run.
