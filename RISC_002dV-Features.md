---
tip: translate by openai@2023-06-23 12:30:53
...
---
description: RISC-V Features (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: RISC-V Features (Debugging with GDB)
lang: en
resource-type: document
title: RISC-V Features (Debugging with GDB)
-------------------------------------------

::: header
Next: [RX Features](RX-Features.html#RX-Features)]
:::

---

#### G.5.13 RISC-V Features

The '`org.gnu.gdb.riscv.cpu`', etc).

> "org.gnu.gdb.riscv.cpu"等

The '`org.gnu.gdb.riscv.fpu`'. As with the cpu feature, either the architectural register names, or the ABI names can be used.

> 'org.gnu.gdb.riscv.fpu'。与 CPU 特性一样，可以使用架构寄存器名称或 ABI 名称。

The '`org.gnu.gdb.riscv.virtual`' register that contains the target's privilege level in the least significant two bits.

> 这个'org.gnu.gdb.riscv.virtual'寄存器包含目标特权级别的最低两位。

The '`org.gnu.gdb.riscv.csr`' registers could be in either feature. The expectation is that these registers will be in the fpu feature if the target has floating point hardware, but can be moved into the csr feature if the target has the floating point control registers, but no other floating point hardware.

> `org.gnu.gdb.riscv.csr` 寄存器可以存在于两种功能中。期望这些寄存器如果目标具有浮点硬件，则会存在于 fpu 功能中，但如果目标具有浮点控制寄存器，但没有其他浮点硬件，则可以移动到 csr 功能中。

The '`org.gnu.gdb.riscv.vector`', all of which must be the same size.

> 'org.gnu.gdb.riscv.vector'，所有的都必须是相同的大小。

---

::: header
Next: [RX Features](RX-Features.html#RX-Features)]
:::
