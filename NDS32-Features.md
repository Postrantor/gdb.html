---
tip: translate by openai@2023-06-24 00:32:31
...
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

> 注意：前16个64位双精度浮点寄存器与32个32位单精度浮点寄存器重叠。32位单精度寄存器如果没有明确列出，将从重叠的64位双精度寄存器的一半中综合出来。明确列出32位单精度寄存器是不推荐的，支持它的功能有一天可能会完全移除。
