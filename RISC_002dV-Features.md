---
tip: translate by openai@2023-06-24 02:14:19
...
---
description: RISC-V Features (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: RISC-V Features (Debugging with GDB)
lang: en
resource-type: document
title: RISC-V Features (Debugging with GDB)
---
::: header
Next: [RX Features](RX-Features.html#RX-Features)]
:::

---

#### G.5.13 RISC-V Features

The '`org.gnu.gdb.riscv.cpu`', etc).


The '`org.gnu.gdb.riscv.fpu`'. As with the cpu feature, either the architectural register names, or the ABI names can be used.

> 'org.gnu.gdb.riscv.fpu'，就像cpu功能一样，可以使用架构寄存器名称或ABI名称。


The '`org.gnu.gdb.riscv.virtual`' register that contains the target's privilege level in the least significant two bits.

> 'org.gnu.gdb.riscv.virtual'寄存器中最低有效两位包含目标的特权级别。


The '`org.gnu.gdb.riscv.csr`' registers could be in either feature. The expectation is that these registers will be in the fpu feature if the target has floating point hardware, but can be moved into the csr feature if the target has the floating point control registers, but no other floating point hardware.

> “org.gnu.gdb.riscv.csr”寄存器可以位于任一特性中。预期如果目标有浮点硬件，这些寄存器将位于fpu特性中，但如果目标有浮点控制寄存器，但没有其它浮点硬件，则可以将它们移动到csr特性中。

The '`org.gnu.gdb.riscv.vector`', all of which must be the same size.

---

::: header
Next: [RX Features](RX-Features.html#RX-Features)]
:::
