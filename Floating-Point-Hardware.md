---
tip: translate by openai@2023-06-23 21:12:54
...
---
description: Floating Point Hardware (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Floating Point Hardware (Debugging with GDB)
lang: en
resource-type: document
title: Floating Point Hardware (Debugging with GDB)
---
::: header
Next: [Vector Unit](Vector-Unit.html#Vector-Unit)]
:::

---

### 10.15 Floating Point Hardware


Depending on the configuration, [GDB] may be able to give you more information about the status of the floating point hardware.

> 根据配置，GDB可能能够提供更多关于浮点硬件状态的信息。

`info float`


Display hardware-dependent information about the floating point unit. The exact contents and layout vary depending on the floating point chip. Currently, '`info float`' is supported on the ARM and x86 machines.

> 显示与浮点单元相关的硬件信息。具体内容和布局取决于浮点芯片。目前，'`info float`'支持ARM和x86机器。
