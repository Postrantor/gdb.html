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

```
`parameter…` as a comma-delimited list. All values are transmitted in ASCII string representation, pointer/length pairs separated by a slash.
```
