---
tip: translate by openai@2023-06-23 18:35:00
...
---
description: Byte Order (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Byte Order (Debugging with GDB)
lang: en
resource-type: document
title: Byte Order (Debugging with GDB)
---
::: header
Previous: [Target Commands](Target-Commands.html#Target-Commands)]
:::

---

### 19.3 Choosing Target Byte Order


Some types of processors, such as the MIPS, PowerPC, and Renesas SH, offer the ability to run either big-endian or little-endian byte orders. Usually the executable or symbol will include a bit to designate the endian-ness, and you will not need to worry about which to use. However, you may still find it useful to adjust [GDB]'s idea of processor endian-ness manually.

> 一些处理器类型，如MIPS、PowerPC和Renesas SH，可以支持大端或小端字节顺序。通常可执行文件或符号会包含一个位来指定端序，你不需要担心哪种要用。然而，你仍然可能需要手动调整GDB的处理器端序。

`set endian big`


Instruct [GDB] to assume the target is big-endian.

> 指示GDB假定目标为大端。

`set endian little`


Instruct [GDB] to assume the target is little-endian.

> 指示GDB假定目标为小端。

`set endian auto`


Instruct [GDB] to use the byte order associated with the executable.

> 指示GDB使用与可执行文件相关联的字节顺序。

`show endian`


Display [GDB]'s current idea of the target byte order.

> 显示GDB当前对目标字节顺序的理解。


If the `set endian auto` mode is in effect and no executable has been selected, then the endianness used is the last one chosen either by one of the `set endian big` and `set endian little` commands or by inferring from the last executable used. If no endianness has been previously chosen, then the default for this mode is inferred from the target [GDB] has been built for, and is `little` if the name of the target CPU has an `el` suffix and `big` otherwise.

> 如果“set endian auto”模式正在生效，且没有选择可执行文件，则所使用的字节序是由“set endian big”和“set endian little”命令之一或从上一个可执行文件中推断出的最后一个选择的字节序。如果以前没有选择过字节序，则此模式的默认值将从[GDB]的目标系统中推断出来，如果目标CPU的名称有“el”后缀，则为“little”，否则为“big”。


Note that these commands merely adjust interpretation of symbolic data on the host, and that they have absolutely no effect on the target system.

> 注意，这些命令仅调整主机上符号数据的解释，对目标系统没有任何影响。
