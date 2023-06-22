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

`info float`

Display hardware-dependent information about the floating point unit. The exact contents and layout vary depending on the floating point chip. Currently, '`info float`' is supported on the ARM and x86 machines.
