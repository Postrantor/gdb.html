---
tip: translate by openai@2023-06-24 00:35:12
...
---
description: Notification Packets (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Notification Packets (Debugging with GDB)
lang: en
resource-type: document
title: Notification Packets (Debugging with GDB)
---
::: header
Next: [Remote Non-Stop](Remote-Non_002dStop.html#Remote-Non_002dStop)]
:::

---

### E.9 Notification Packets


The [GDB] remote serial protocol includes *notifications*, packets that require no acknowledgment. Both the GDB and the stub may send notifications (although the only notifications defined at present are sent by the stub). Notifications carry information without incurring the round-trip latency of an acknowledgment, and so are useful for low-impact communications where occasional packet loss is not a problem.

> 远程串行协议（GDB）包括*通知*，无需确认的数据包。GDB和存根都可以发送通知（尽管目前定义的通知仅由存根发送）。通知传输信息而不需要回程时延，因此对于偶尔丢包不成问题的低影响通信非常有用。


A notification packet has the form '`% data # checksum`' to acknowledge the notification's receipt or to report its corruption.

> 通知数据包的格式为 '% data # checksum'，以确认收到通知或报告其损坏。


Every notification's `data` begins with a name, which contains no colon characters, followed by a colon character.

> 每个通知的`数据`都以一个不包含冒号的名称开头，后面跟着一个冒号。


Recipients should silently ignore corrupted notifications and notifications they do not understand. Recipients should restart timeout periods on receipt of a well-formed notification, whether or not they understand it.

> 接收者应该静默地忽略损坏的通知和他们不理解的通知。 接收者应该在收到格式正确的通知时重新启动超时期，无论他们是否理解它。


Senders should only send the notifications described here when this protocol description specifies that they are permitted. In the future, we may extend the protocol to permit existing notifications in new contexts; this rule helps older senders avoid confusing newer recipients.

> 发送者只有在本协议描述指定允许时，才能发送描述在此处的通知。将来，我们可能会扩展该协议，以允许在新的上下文中使用现有的通知；此规则有助于较旧的发送者避免让较新的接收者感到困惑。


(Older versions of [GDB] to send at the moment, but we assume that most older stubs would ignore them, as well.)

> （我们假设大多数较旧的存根会忽略它们，但目前还可以发送较旧版本的GDB。）

Each notification is comprised of three parts:

'`name:event`'


:   The notification packet is sent by the side that initiates the exchange (currently, only the stub does that), with `event` specifying the name of the notification.

> 通知数据包是由发起交换的一方（目前只有存根）发送的，其中的`event`指定通知的名称。

'`ack`'


:   The acknowledge sent by the other side, usually [GDB], to acknowledge the exchange and request the event.

> 另一方发送的确认，通常是[GDB]，以确认交换并请求事件。


The purpose of an asynchronous notification mechanism is to report to [GDB] that something interesting happened in the remote stub.

> 异步通知机制的目的是向[GDB]报告远程存根中发生了有趣的事情。

The remote stub may send notification `name` may not have received it.


Specifically, notifications may appear when [GDB]' acknowledgment to a packet it has sent. Notification packets are distinct from any other communication from the stub so there is no ambiguity.

> 具体而言，当GDB收到它发送的数据包时，可能会出现通知。通知数据包与来自存根的任何其他通信不同，因此没有模棱两可。


After receiving a notification, [GDB] is permitted to send other, unrelated packets to the stub first, which the stub should process normally.

> 收到通知后，GDB有权先向存根发送其他不相关的数据包，存根应正常处理这些数据包。


Upon receiving a `ack` packet to solicit further responses; again, it is permitted to send other, unrelated packets as well which the stub should process normally.

> 收到一个“ack”数据包以请求进一步响应时，也可以发送其他与之无关的数据包，存根应当正常处理这些数据包。


If the stub receives a `ack` shall accept the notification, and the process shall be repeated.

> 如果桩收到一个`ack`，应接受通知，并重复该过程。


The process of asynchronous notification can be illustrated by the following example:

> 例如，可以用下面的例子来说明异步通知的过程：

::: smallexample

```bash
<- %Stop:T0505:98e7ffbf;04:4ce6ffbf;08:b1b6e54c;thread:p7526.7526;core:0;
...
-> vStopped
<- T0505:68f37db7;04:40f37db7;08:63850408;thread:p7526.7528;core:0;
-> vStopped
<- T0505:68e3fdb6;04:40e3fdb6;08:63850408;thread:p7526.7529;core:0;
-> vStopped
<- OK
```

:::

The following notifications are defined:

---


Notification   Ack        Event                                                                                                                                                                                                                                                                                                                Description

> 通知确认事件描述

Stop           vStopped   `reply`.   Report an asynchronous stop event in non-stop mode.

> 停止vStopped回复。在非停止模式下报告一个异步停止事件。

---

---

::: header
Next: [Remote Non-Stop](Remote-Non_002dStop.html#Remote-Non_002dStop)]
:::
