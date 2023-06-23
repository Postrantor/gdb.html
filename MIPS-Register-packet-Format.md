---
description: MIPS Register packet Format (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: MIPS Register packet Format (Debugging with GDB)
lang: en
resource-type: document
title: MIPS Register packet Format (Debugging with GDB)
---
::: header
Next: [MIPS Breakpoint Kinds](MIPS-Breakpoint-Kinds.html#MIPS-Breakpoint-Kinds)]
:::

---

#### E.5.2.1 MIPS Register Packet Format

The following `g`/`G` packets have previously been defined. In the below, some thirty-two bit registers are transferred as sixty-four bits. Those registers should be zero/sign extended (which?) to fill the space allocated. Register bytes are transferred in target byte order. The two nibbles within a register byte are transferred most-significant -- least-significant.

[MIPS32]

:   All registers are transferred as thirty-two bit quantities in the order: 32 general-purpose; sr; lo; hi; bad; cause; pc; 32 floating-point registers; fsr; fir; fp.

[MIPS64]

:   All registers are transferred as sixty-four bit quantities (including thirty-two bit registers such as `sr`). The ordering is the same as `MIPS32`.
