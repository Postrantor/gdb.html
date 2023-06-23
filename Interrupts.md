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

'`Ctrl-C`' packet (see [X packet](Packets.html#X-packet)), used for binary downloads, may include an unescaped `0x03` as part of its packet.

`BREAK` followed by `g` is also known as Magic SysRq g. When Linux kernel receives this sequence from serial port, it stops execution and connects to gdb.

In non-stop mode, because packet resumptions are asynchronous (see [vCont packet](Packets.html#vCont-packet)), [GDB] instead sends a regular packet (see [vCtrlC packet](Packets.html#vCtrlC-packet)) with the usual packet framing instead of the single byte `0x03`.

Stubs are not required to recognize these interrupt mechanisms and the precise meaning associated with receipt of the interrupt is implementation defined. If the target supports debugging of multiple threads and/or processes, it should attempt to interrupt all currently-executing threads and processes. If the stub is successful at interrupting the running program, it should send one of the stop reply packets (see [Stop Reply Packets](Stop-Reply-Packets.html#Stop-Reply-Packets)) to [GDB] as a result of successfully stopping the program in all-stop mode, and a stop reply for each stopped thread in non-stop mode. Interrupts received while the program is stopped are queued and the program will be interrupted when it is resumed next time.

---

::: header
Next: [Notification Packets](Notification-Packets.html#Notification-Packets)]
:::
