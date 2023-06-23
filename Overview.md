---
description: Overview (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Overview (Debugging with GDB)
lang: en
resource-type: document
title: Overview (Debugging with GDB)
---
::: header
Next: [Packets](Packets.html#Packets)]
:::

---

### E.1 Overview

There may be occasions when you need to know something about the protocol---for example, if there is only one serial port to your target machine, you might want your program to do something special if it recognizes a packet meant for [GDB].

In the examples below, '`->`' are used to indicate transmitted and received data, respectively.

All [GDB]:

::: smallexample

```bash
$packet-data#checksum
```

:::

The two-digit `checksum`' (an eight bit unsigned checksum).

Implementors should note that prior to [GDB]:

::: smallexample

```bash
$sequence-id:packet-data#checksum
```

:::

That `sequence-id`.

When either the host or the target machine receives a packet, the first response expected is an acknowledgment: either '`+`' (to request retransmission):

::: smallexample

```bash
-> $packet-data#checksum
<- +
```

:::

The '`+`' acknowledgments can be disabled once a connection is established. See [Packet Acknowledgment](Packet-Acknowledgment.html#Packet-Acknowledgment), for details.

The host ([GDB]'s non-stop execution mode; see [Remote Non-Stop](Remote-Non_002dStop.html#Remote-Non_002dStop), for details.

`packet-data`' packet for additional exceptions).

Fields within the packet should be separated using '`,` with leading zeros suppressed.

Implementors should note that prior to [GDB]).

Binary data in most packets is encoded either as two hexadecimal digits per byte of binary data. This allowed the traditional remote protocol to work over connections which were only seven-bit clean. Some packets designed more recently assume an eight-bit clean connection, and use a more efficient encoding to send and receive binary data.

The binary data representation uses `7d` ([ASCII]'), so that it is not interpreted as the start of a run-length encoded sequence (described next).

Response `data`' means repeat the leading `0` `32 - 29 = 3` more times.

The printable characters '`#`'.

The error response returned for some packets includes a two character error number. That number is not well defined.

For any `command` can tell if a packet is supported based on that response.

At a minimum, a stub is required to support the '`?`' command. All other commands are optional.

---

::: header
Next: [Packets](Packets.html#Packets)]
:::
