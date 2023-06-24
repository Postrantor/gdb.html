---
tip: translate by openai@2023-06-24 00:21:39
...
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

> 微控制器是一种支持各种Xilinx FPGA（如Spartan或Virtex系列）的软核处理器。搭载这些处理器的板子通常具有与主机系统连接的JTAG端口，主机系统运行Xilinx嵌入式开发套件（EDK）或软件开发套件（SDK）。该主机系统用于将配置位流下载到目标FPGA。Xilinx微处理器调试器（XMD）程序使用JTAG接口与目标板通信，并向板上提供“gdbserver”接口。默认情况下，`xmd`使用端口`1234`。（尽管可以更改此默认端口，但需要使用未公开的`xmd`命令。如果需要这样做，请联系Xilinx支持。）

Use these GDB commands to connect to the MicroBlaze target processor.

`target remote :1234`


:   Use this command to connect to the target if you are running [GDB] on the same system as `xmd`.

> 使用这个命令，如果你在和`xmd`同一台系统上运行[GDB]，就可以连接到目标。

`target remote xmd-host:1234`


:   Use this command to connect to the target if it is connected to `xmd` running on a different system named `xmd-host`.

> 使用这个命令连接到目标，如果它连接到运行在另一台名为`xmd-host`的系统上的`xmd`。

`load`

:   Use this command to download a program to the MicroBlaze target.

`set debug microblaze n`

:   Enable MicroBlaze-specific debugging messages if non-zero.

`show debug microblaze n`

:   Show MicroBlaze-specific debugging level.
