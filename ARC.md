---
tip: translate by openai@2023-06-23 17:19:15
...
---
description: ARC (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: ARC (Debugging with GDB)
lang: en
resource-type: document
title: ARC (Debugging with GDB)
---
::: header
Next: [ARM](ARM.html#ARM)]
:::

---

#### 21.3.1 Synopsys ARC


[GDB] provides the following ARC-specific commands:

> [GDB] 提供以下特定于 ARC 的命令：

`set debug arc`

:

```
Control the level of ARC specific debug messages. Use 0 for no messages (the default), 1 for debug messages, and 2 for even more debug messages.
```

`show debug arc`

:

```
Show the level of ARC specific debugging in operation.
```

`maint print arc arc-instruction address`

:

```
Print internal disassembler information about instruction at a given address.
```
