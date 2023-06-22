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

[GDB]' packet as necessary to probe the target state after a mode change.

In non-stop mode, when an attached process encounters an event that would otherwise be reported with a stop reply, it uses the asynchronous notification mechanism (see [Notification Packets](Notification-Packets.html#Notification-Packets)) to inform [GDB]' response, all running threads belonging to other attached processes continue to run.

In non-stop mode, the target shall respond to the '`?`'.

If the stub supports non-stop mode, it should also support the '`swbreak`' feature implies that the target is responsible for adjusting the PC when a software breakpoint triggers, if necessary, such as on the x86 architecture.

---

::: header
Next: [Packet Acknowledgment](Packet-Acknowledgment.html#Packet-Acknowledgment)]
:::
