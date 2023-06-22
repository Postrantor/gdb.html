---
description: NDS32 Features (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: NDS32 Features (Debugging with GDB)
lang: en
resource-type: document
title: NDS32 Features (Debugging with GDB)
---
::: header
Next: [Nios II Features](Nios-II-Features.html#Nios-II-Features)]
:::

---

#### G.5.9 NDS32 Features

The '`org.gnu.gdb.nds32.core`'.

The '`org.gnu.gdb.nds32.fpu`' based on the FPU configuration implemented.

*Note:* The first sixteen 64-bit double-precision floating-point registers are overlapped with the thirty-two 32-bit single-precision floating-point registers. The 32-bit single-precision registers, if not being listed explicitly, will be synthesized from halves of the overlapping 64-bit double-precision registers. Listing 32-bit single-precision registers explicitly is deprecated, and the support to it could be totally removed some day.
