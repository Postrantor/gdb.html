---
tip: translate by openai@2023-06-23 20:50:29
...
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

> 这些命令已弃用；它们等同于普通的“disable”和“enable”。

`disable tracepoint [num]`


Disable tracepoint `num` is given. A disabled tracepoint will have no effect during a trace experiment, but it is not forgotten. You can re-enable a disabled tracepoint using the `enable tracepoint` command. If the command is issued during a trace experiment and the debug target has support for disabling tracepoints during a trace experiment, then the change will be effective immediately. Otherwise, it will be applied to the next trace experiment.

> 禁用跟踪点`num`已给出。禁用的跟踪点在跟踪实验期间不会产生任何效果，但不会被遗忘。您可以使用`enable tracepoint`命令重新启用禁用的跟踪点。如果在跟踪实验期间发出该命令，而调试目标支持在跟踪实验期间禁用跟踪点，则更改将立即生效。否则，它将应用于下一个跟踪实验。

`enable tracepoint [num]`


Enable tracepoint `num`, or all tracepoints. If this command is issued during a trace experiment and the debug target supports enabling tracepoints during a trace experiment, then the enabled tracepoints will become effective immediately. Otherwise, they will become effective the next time a trace experiment is run.

> 启用断点`num`，或者所有断点。如果在跟踪实验期间发出此命令，且调试目标支持在跟踪实验期间启用断点，则已启用的断点将立即生效。否则，它们将在下次运行跟踪实验时生效。
