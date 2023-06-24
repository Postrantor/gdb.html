---
tip: translate by openai@2023-06-23 23:34:25
...
---
description: Interrupts (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Interrupts (Debugging with GDB)
lang: en
resource-type: document
title: Interrupts (Debugging with GDB)
---
::: header
Next: [Notification Packets](Notification-Packets.html#Notification-Packets)]
:::

---

### E.8 Interrupts

In all-stop mode, when a program on the remote target is running, [GDB]'.


The precise meaning of `BREAK` is defined by the transport mechanism and may, in fact, be undefined. [GDB] sends the `telnet` BREAK sequence.

> 精确的`BREAK`的含义由传输机制定义，实际上可能没有定义。[GDB]发送`telnet` BREAK序列。


'`Ctrl-C`' packet (see [X packet](Packets.html#X-packet)), used for binary downloads, may include an unescaped `0x03` as part of its packet.

> `Ctrl-C` 包（参见 [X 包](Packets.html#X-packet)），用于二进制下载，可能包含一个未转义的 `0x03` 作为其包的一部分。

`BREAK` followed by `g` is also known as Magic SysRq g. When Linux kernel receives this sequence from serial port, it stops execution and connects to gdb.


In non-stop mode, because packet resumptions are asynchronous (see [vCont packet](Packets.html#vCont-packet)), [GDB] instead sends a regular packet (see [vCtrlC packet](Packets.html#vCtrlC-packet)) with the usual packet framing instead of the single byte `0x03`.

> 在不停止模式下，由于数据包恢复是异步的（参见[vCont数据包](Packets.html#vCont-packet)），[GDB]而是发送带有通常数据包帧的常规数据包（参见[vCtrlC数据包](Packets.html#vCtrlC-packet）而不是单字节`0x03`。


Stubs are not required to recognize these interrupt mechanisms and the precise meaning associated with receipt of the interrupt is implementation defined. If the target supports debugging of multiple threads and/or processes, it should attempt to interrupt all currently-executing threads and processes. If the stub is successful at interrupting the running program, it should send one of the stop reply packets (see [Stop Reply Packets](Stop-Reply-Packets.html#Stop-Reply-Packets)) to [GDB] as a result of successfully stopping the program in all-stop mode, and a stop reply for each stopped thread in non-stop mode. Interrupts received while the program is stopped are queued and the program will be interrupted when it is resumed next time.

> 不需要存根来识别这些中断机制及收到中断时所关联的精确含义，其实现定义。如果目标支持多线程和/或进程的调试，它应该尝试中断所有当前正在执行的线程和进程。如果存根成功地中断正在运行的程序，它应该发送一个停止回复数据包（参见[停止回复数据包]（Stop-Reply-Packets.html#Stop-Reply-Packets））给GDB，作为成功停止所有停止模式下的程序的结果，以及非停止模式下每个停止的线程的停止回复。当程序停止时收到的中断会被排队，程序在下次恢复时会被中断。

---

::: header
Next: [Notification Packets](Notification-Packets.html#Notification-Packets)]
:::
