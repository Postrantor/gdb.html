---
tip: translate by openai@2023-06-24 02:05:37
...
---
description: Remote Non-Stop (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Remote Non-Stop (Debugging with GDB)
lang: en
resource-type: document
title: Remote Non-Stop (Debugging with GDB)
---
::: header
Next: [Packet Acknowledgment](Packet-Acknowledgment.html#Packet-Acknowledgment)]
:::

---

### E.10 Remote Protocol Support for Non-Stop Mode


[GDB]' response (see [qSupported](General-Query-Packets.html#qSupported)).

> [GDB]：支持的功能：multiprocess+;swbreak+;hwbreak+;qRelocInsn+;fork-events+;vfork-events+;exec-events+;vContSupported+;QThreadEvents+;no-resumed+;xmlRegisters=i386

[GDB]' packet as necessary to probe the target state after a mode change.


In non-stop mode, when an attached process encounters an event that would otherwise be reported with a stop reply, it uses the asynchronous notification mechanism (see [Notification Packets](Notification-Packets.html#Notification-Packets)) to inform [GDB]' response, all running threads belonging to other attached processes continue to run.

> 在不停止模式下，当一个附加的进程遇到一个原本会用停止回复报告的事件时，它会使用异步通知机制（参见[通知包](Notification-Packets.html#Notification-Packets)）来通知[GDB]，所有属于其他附加进程的正在运行的线程将继续运行。

In non-stop mode, the target shall respond to the '`?`'.


If the stub supports non-stop mode, it should also support the '`swbreak`' feature implies that the target is responsible for adjusting the PC when a software breakpoint triggers, if necessary, such as on the x86 architecture.

> 如果存根支持非停止模式，它也应该支持“swbreak”功能，这意味着目标负责在软件断点触发时，如果有必要，调整PC，例如在x86架构上。

---

::: header
Next: [Packet Acknowledgment](Packet-Acknowledgment.html#Packet-Acknowledgment)]
:::
