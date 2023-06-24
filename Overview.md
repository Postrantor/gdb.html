---
tip: translate by openai@2023-06-24 00:58:18
...
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

> 可能会有时候你需要了解一些关于协议的信息---例如，如果你的目标机器只有一个串行端口，你可能希望你的程序如果能识别出一个用于[GDB]的数据包时做出一些特殊的处理。


In the examples below, '`->`' are used to indicate transmitted and received data, respectively.

> 在下面的示例中，'->' 用于表示传输和接收的数据，分别表示。

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

> 当主机或目标机接收到一个数据包时，首先期望的响应是确认：'+'（要求重新传输）：

::: smallexample

```bash
-> $packet-data#checksum
<- +
```

:::


The '`+`' acknowledgments can be disabled once a connection is established. See [Packet Acknowledgment](Packet-Acknowledgment.html#Packet-Acknowledgment), for details.

> '+'确认可以在建立连接后禁用。有关详细信息，请参阅[数据包确认](Packet-Acknowledgment.html#Packet-Acknowledgment)。


The host ([GDB]'s non-stop execution mode; see [Remote Non-Stop](Remote-Non_002dStop.html#Remote-Non_002dStop), for details.

> 主机（GDB的非停止执行模式；详见[远程非停止](Remote-Non_002dStop.html#Remote-Non_002dStop)），有关详情。

`packet-data`' packet for additional exceptions).


Fields within the packet should be separated using '`,` with leading zeros suppressed.

> 包内的字段应该使用“，”隔开，前导零应该被忽略。

Implementors should note that prior to [GDB]).


Binary data in most packets is encoded either as two hexadecimal digits per byte of binary data. This allowed the traditional remote protocol to work over connections which were only seven-bit clean. Some packets designed more recently assume an eight-bit clean connection, and use a more efficient encoding to send and receive binary data.

> 二进制数据在大多数数据包中通常以每字节两个十六进制数字编码。这使传统的远程协议可以在仅有七位清晰度的连接上工作。最近设计的一些数据包假设具有八位清晰度的连接，并使用更有效的编码来发送和接收二进制数据。


The binary data representation uses `7d` ([ASCII]'), so that it is not interpreted as the start of a run-length encoded sequence (described next).

> 二进制数据表示使用`7d`（[ASCII]），以免被解释为下一步运行长度编码序列（描述如下）的开始。

Response `data`' means repeat the leading `0` `32 - 29 = 3` more times.

The printable characters '`#`'.


The error response returned for some packets includes a two character error number. That number is not well defined.

> 返回给某些数据包的错误响应包含两个字符的错误号。这个号码没有得到很好的定义。


For any `command` can tell if a packet is supported based on that response.

> 对于任何`命令`，都可以根据响应来判断是否支持该数据包。


At a minimum, a stub is required to support the '`?`' command. All other commands are optional.

> 至少需要一个存根来支持'`？`'命令。其他命令是可选的。

---

::: header
Next: [Packets](Packets.html#Packets)]
:::
