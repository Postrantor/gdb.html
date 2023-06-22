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

The '`org.gnu.gdb.riscv.virtual`' register that contains the target's privilege level in the least significant two bits.

The '`org.gnu.gdb.riscv.csr`' registers could be in either feature. The expectation is that these registers will be in the fpu feature if the target has floating point hardware, but can be moved into the csr feature if the target has the floating point control registers, but no other floating point hardware.

The '`org.gnu.gdb.riscv.vector`', all of which must be the same size.

---

::: header
Next: [RX Features](RX-Features.html#RX-Features)]
:::
