---
description: OpenRISC 1000 (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: OpenRISC 1000 (Debugging with GDB)
lang: en
resource-type: document
title: OpenRISC 1000 (Debugging with GDB)
---
::: header
Next: [PowerPC Embedded](PowerPC-Embedded.html#PowerPC-Embedded)]
:::

---

#### 21.3.7 OpenRISC 1000

The OpenRISC 1000 provides a free RISC instruction set architecture. It is mainly provided as a soft-core which can run on Xilinx, Altera and other FPGA's.

[GDB] for OpenRISC supports the below commands when connecting to a target:

`target sim`

Runs the builtin CPU simulator which can run very basic programs but does not support most hardware functions like MMU. For more complex use cases the user is advised to run an external target, and connect using '`target remote`'.

Example: `target sim`

`set debug or1k`

Toggle whether to display OpenRISC-specific debugging messages from the OpenRISC target support subsystem.

`show debug or1k`

Show whether OpenRISC-specific debugging messages are enabled.
