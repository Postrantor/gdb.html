---
tip: translate by openai@2023-06-23 13:24:16
...
---
description: Sparc Features (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Sparc Features (Debugging with GDB)
lang: en
resource-type: document
title: Sparc Features (Debugging with GDB)
---
::: header
Next: [TIC6x Features](TIC6x-Features.html#TIC6x-Features)]
:::

---

#### G.5.16 Sparc Features


The '`org.gnu.gdb.sparc.cpu`' feature is required for sparc32/sparc64 targets. It should describe the following registers:

> 要使用sparc32/sparc64目标，需要'org.gnu.gdb.sparc.cpu'特性。它应该描述以下寄存器：

- \- '`g0`'
- \- '`o0`'
- \- '`l0`'
- \- '`i0`'


They may be 32-bit or 64-bit depending on the target.

> 它们可能是32位或64位，取决于目标。


Also the '`org.gnu.gdb.sparc.fpu`' feature is required for sparc32/sparc64 targets. It should describe the following registers:

> 对于sparc32/sparc64目标，还需要`org.gnu.gdb.sparc.fpu`特性。它应该描述以下寄存器：

- \- '`f0`'
- \- '`f32`' for sparc64


The '`org.gnu.gdb.sparc.cp0`' feature is required for sparc32/sparc64 targets. It should describe the following registers:

> 对于sparc32/sparc64目标，需要“org.gnu.gdb.sparc.cp0”特性。它应该描述以下寄存器：

- \- '`y`' for sparc32
- \- '`pc`' for sparc64
