---
tip: translate by openai@2023-06-24 00:23:21
...
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

> 以下`g`/`G`封包已经定义好。在下面，一些32位寄存器会被传输成64位。这些寄存器应该被零/符号扩展（哪一个？）来填充已分配的空间。寄存器字节以目标字节顺序传输。寄存器字节内的两个半字节以最高有效位-最低有效位的顺序传输。

[MIPS32]


:   All registers are transferred as thirty-two bit quantities in the order: 32 general-purpose; sr; lo; hi; bad; cause; pc; 32 floating-point registers; fsr; fir; fp.

> 所有寄存器以32位量的顺序传输：32个通用寄存器；sr；lo；hi；bad；cause；pc；32个浮点寄存器；fsr；fir；fp。

[MIPS64]


:   All registers are transferred as sixty-four bit quantities (including thirty-two bit registers such as `sr`). The ordering is the same as `MIPS32`.

> 所有寄存器都以64位量传输（包括32位寄存器，如'sr'）。顺序与MIPS32相同。
