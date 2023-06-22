---
description: PowerPC (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: PowerPC (Debugging with GDB)
lang: en
resource-type: document
title: PowerPC (Debugging with GDB)
---
::: header
Next: [Nios II](Nios-II.html#Nios-II)]
:::

---

#### 21.4.6 PowerPC

When [GDB] is debugging the PowerPC architecture, it provides a set of pseudo-registers to enable inspection of 128-bit wide Decimal Floating Point numbers stored in the floating point registers. These values must be stored in two consecutive registers, always starting at an even register like `f0` or `f2`.

The pseudo-registers go from `$dl0` through `$dl15`, and are formed by joining the even/odd register pairs `f0` and `f1` for `$dl0`, `f2` and `f3` for `$dl1` and so on.

For POWER7 processors, [GDB]').
