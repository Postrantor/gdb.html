---
tip: translate by openai@2023-06-24 01:07:30
...
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

> 当[GDB]调试PowerPC架构时，它提供了一组伪寄存器，以便检查存储在浮点寄存器中的128位宽十进制浮点数。这些值必须存储在连续的寄存器中，始终从偶数寄存器（如'f0'或'f2'）开始。


The pseudo-registers go from `$dl0` through `$dl15`, and are formed by joining the even/odd register pairs `f0` and `f1` for `$dl0`, `f2` and `f3` for `$dl1` and so on.

> 伪寄存器从$dl0开始，一直到$dl15，它们是通过偶数/奇数寄存器对f0和f1形成的$dl0，f2和f3形成的$dl1以此类推来构成的。

For POWER7 processors, [GDB]').
