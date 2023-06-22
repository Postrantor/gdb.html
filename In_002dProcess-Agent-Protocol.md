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

---

• [IPA Protocol Objects](IPA-Protocol-Objects.html#IPA-Protocol-Objects):        
• [IPA Protocol Commands](IPA-Protocol-Commands.html#IPA-Protocol-Commands):     

---
