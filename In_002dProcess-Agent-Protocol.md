---
tip: translate by openai@2023-06-23 23:37:46
...
---
description: In-Process Agent Protocol (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: In-Process Agent Protocol (Debugging with GDB)
lang: en
resource-type: document
title: In-Process Agent Protocol (Debugging with GDB)
---
::: header
Up: [In-Process Agent](In_002dProcess-Agent.html#In_002dProcess-Agent)]
:::

---

### 31.1 In-Process Agent Protocol


The in-process agent is able to communicate with both [GDB] or GDBserver sends commands (see [IPA Protocol Commands](IPA-Protocol-Commands.html#IPA-Protocol-Commands)) and data to in-process agent, and then in-process agent replies back with the return result of the command, or some other information. The data sent to in-process agent is composed of primitive data types, such as 4-byte or 8-byte type, and composite types, which are called objects (see [IPA Protocol Objects](IPA-Protocol-Objects.html#IPA-Protocol-Objects)).

> 代理进程能够与GDB或GDBserver进行通信（参见[IPA协议命令]（IPA-Protocol-Commands.html#IPA-Protocol-Commands））并发送命令和数据到代理进程，然后代理进程会回复命令的返回结果或其他信息。发送到代理进程的数据由原始数据类型（如4字节或8字节类型）和称为对象的复合类型（参见[IPA协议对象]（IPA-Protocol-Objects.html#IPA-Protocol-Objects））组成。

---


• [IPA Protocol Objects](IPA-Protocol-Objects.html#IPA-Protocol-Objects):        

> •[IPA协议对象](IPA-Protocol-Objects.html#IPA-Protocol-Objects):

• [IPA Protocol Commands](IPA-Protocol-Commands.html#IPA-Protocol-Commands):     

> • [IPA 协议命令](IPA-Protocol-Commands.html#IPA-Protocol-Commands):

---
