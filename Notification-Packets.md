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

A notification packet has the form '`% data # checksum`' to acknowledge the notification's receipt or to report its corruption.

Every notification's `data` begins with a name, which contains no colon characters, followed by a colon character.

Recipients should silently ignore corrupted notifications and notifications they do not understand. Recipients should restart timeout periods on receipt of a well-formed notification, whether or not they understand it.

Senders should only send the notifications described here when this protocol description specifies that they are permitted. In the future, we may extend the protocol to permit existing notifications in new contexts; this rule helps older senders avoid confusing newer recipients.

(Older versions of [GDB] to send at the moment, but we assume that most older stubs would ignore them, as well.)

Each notification is comprised of three parts:

'`name:event`'

:   The notification packet is sent by the side that initiates the exchange (currently, only the stub does that), with `event` specifying the name of the notification.

'`ack`'

:   The acknowledge sent by the other side, usually [GDB], to acknowledge the exchange and request the event.

The purpose of an asynchronous notification mechanism is to report to [GDB] that something interesting happened in the remote stub.

The remote stub may send notification `name` may not have received it.

Specifically, notifications may appear when [GDB]' acknowledgment to a packet it has sent. Notification packets are distinct from any other communication from the stub so there is no ambiguity.

After receiving a notification, [GDB] is permitted to send other, unrelated packets to the stub first, which the stub should process normally.

Upon receiving a `ack` packet to solicit further responses; again, it is permitted to send other, unrelated packets as well which the stub should process normally.

If the stub receives a `ack` shall accept the notification, and the process shall be repeated.

The process of asynchronous notification can be illustrated by the following example:

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
Stop           vStopped   `reply`.   Report an asynchronous stop event in non-stop mode.

---

---

::: header
Next: [Remote Non-Stop](Remote-Non_002dStop.html#Remote-Non_002dStop)]
:::
