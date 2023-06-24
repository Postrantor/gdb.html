---
tip: translate by openai@2023-06-24 00:59:36
...
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

> 默认情况下，当主机或目标机接收到一个数据包时，首先预期的响应是确认：要么是“远程协议”，要么是在不可靠的传输机制（如串行线路）上运行的。


In cases where the transport mechanism is itself reliable (such as a pipe or TCP connection), the '`+`' packet; see [QStartNoAckMode](General-Query-Packets.html#QStartNoAckMode).

> 在传输机制本身可靠的情况下（如管道或TCP连接），可以使用'+'数据包；参见[QStartNoAckMode](General-Query-Packets.html#QStartNoAckMode)。


When in no-acknowledgment mode, neither the stub nor [GDB]' protocol acknowledgments. The packet and response format still includes the normal checksum, as described in [Overview](Overview.html#Overview), but the checksum may be ignored by the receiver.

> 当处于无应答模式时，存根和[GDB]协议都不会有应答。数据包和响应格式仍然包括正常的校验和，如[概述](Overview.html#Overview)中所述，但接收者可以忽略校验和。


If the stub supports '`QStartNoAckMode`' response, which can be safely ignored by the stub.

> 如果存根支持'QStartNoAckMode'响应，存根可以安全地忽略它。


Note that `set remote noack-packet` command only affects negotiation between [GDB]' acknowledgments are enabled by default when a new connection is established, there is also no protocol request to re-enable the acknowledgments for the current connection, once disabled.

> 注意，`set remote noack-packet` 命令只影响[GDB]之间的协商，新建立连接时默认启用确认，一旦禁用，也没有协议请求重新启用当前连接的确认。

---

::: header
Next: [Examples](Examples.html#Examples)]
:::
