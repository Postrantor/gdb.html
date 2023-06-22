---
description: MicroBlaze (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: MicroBlaze (Debugging with GDB)
lang: en
resource-type: document
title: MicroBlaze (Debugging with GDB)
---
::: header
Next: [MIPS Embedded](MIPS-Embedded.html#MIPS-Embedded)]
:::

---

#### 21.3.5 MicroBlaze

The MicroBlaze is a soft-core processor supported on various Xilinx FPGAs, such as Spartan or Virtex series. Boards with these processors usually have JTAG ports which connect to a host system running the Xilinx Embedded Development Kit (EDK) or Software Development Kit (SDK). This host system is used to download the configuration bitstream to the target FPGA. The Xilinx Microprocessor Debugger (XMD) program communicates with the target board using the JTAG interface and presents a `gdbserver` interface to the board. By default `xmd` uses port `1234`. (While it is possible to change this default port, it requires the use of undocumented `xmd` commands. Contact Xilinx support if you need to do this.)

Use these GDB commands to connect to the MicroBlaze target processor.

`target remote :1234`

:   Use this command to connect to the target if you are running [GDB] on the same system as `xmd`.

`target remote xmd-host:1234`

:   Use this command to connect to the target if it is connected to `xmd` running on a different system named `xmd-host`.

`load`

:   Use this command to download a program to the MicroBlaze target.

`set debug microblaze n`

:   Enable MicroBlaze-specific debugging messages if non-zero.

`show debug microblaze n`

:   Show MicroBlaze-specific debugging level.
