---
description: Packet Acknowledgment (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Packet Acknowledgment (Debugging with GDB)
lang: en
resource-type: document
title: Packet Acknowledgment (Debugging with GDB)
---
::: header
Next: [Examples](Examples.html#Examples)]
:::

---

### E.11 Packet Acknowledgment

By default, when either the host or the target machine receives a packet, the first response expected is an acknowledgment: either '`+` remote protocol to operate over unreliable transport mechanisms, such as a serial line.

In cases where the transport mechanism is itself reliable (such as a pipe or TCP connection), the '`+`' packet; see [QStartNoAckMode](General-Query-Packets.html#QStartNoAckMode).

When in no-acknowledgment mode, neither the stub nor [GDB]' protocol acknowledgments. The packet and response format still includes the normal checksum, as described in [Overview](Overview.html#Overview), but the checksum may be ignored by the receiver.

If the stub supports '`QStartNoAckMode`' response, which can be safely ignored by the stub.

Note that `set remote noack-packet` command only affects negotiation between [GDB]' acknowledgments are enabled by default when a new connection is established, there is also no protocol request to re-enable the acknowledgments for the current connection, once disabled.

---

::: header
Next: [Examples](Examples.html#Examples)]
:::
