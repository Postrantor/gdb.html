---
tip: translate by openai@2023-06-24 00:45:48
...
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

> 开放RISC 1000提供免费的RISC指令集架构。它主要提供作为一种软核，可以在Xilinx、Altera和其他FPGA上运行。


[GDB] for OpenRISC supports the below commands when connecting to a target:

> [GDB] 为 OpenRISC 支持连接到目标时以下命令：

`target sim`


Runs the builtin CPU simulator which can run very basic programs but does not support most hardware functions like MMU. For more complex use cases the user is advised to run an external target, and connect using '`target remote`'.

> 运行内置的CPU模拟器，可以运行非常基本的程序，但不支持大多数硬件功能，如MMU。对于更复杂的用例，建议用户运行外部目标，并使用“target remote”进行连接。

Example: `target sim`

`set debug or1k`


Toggle whether to display OpenRISC-specific debugging messages from the OpenRISC target support subsystem.

> 切换是否从OpenRISC目标支持子系统显示OpenRISC特定的调试消息。

`show debug or1k`

Show whether OpenRISC-specific debugging messages are enabled.
