---
tip: translate by openai@2023-06-24 03:52:52
...
---
description: The F Request Packet (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: The F Request Packet (Debugging with GDB)
lang: en
resource-type: document
title: The F Request Packet (Debugging with GDB)
---
::: header
Next: [The F Reply Packet](The-F-Reply-Packet.html#The-F-Reply-Packet)]
:::

---

#### E.13.3 The `F` Request Packet

The `F` request packet has the following format:

'`Fcall-id,parameter…`'


:   `call-id` is the identifier to indicate the host system call to be called. This is just the name of the function.

> `call-id`是指示要调用的主机系统调用的标识符。这只是函数的名称。

```
`parameter…` as a comma-delimited list. All values are transmitted in ASCII string representation, pointer/length pairs separated by a slash.
```
