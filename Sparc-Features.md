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

- \- '`g0`'
- \- '`o0`'
- \- '`l0`'
- \- '`i0`'

They may be 32-bit or 64-bit depending on the target.

Also the '`org.gnu.gdb.sparc.fpu`' feature is required for sparc32/sparc64 targets. It should describe the following registers:

- \- '`f0`'
- \- '`f32`' for sparc64

The '`org.gnu.gdb.sparc.cp0`' feature is required for sparc32/sparc64 targets. It should describe the following registers:

- \- '`y`' for sparc32
- \- '`pc`' for sparc64
