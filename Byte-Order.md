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

`set endian big`

Instruct [GDB] to assume the target is big-endian.

`set endian little`

Instruct [GDB] to assume the target is little-endian.

`set endian auto`

Instruct [GDB] to use the byte order associated with the executable.

`show endian`

Display [GDB]'s current idea of the target byte order.

If the `set endian auto` mode is in effect and no executable has been selected, then the endianness used is the last one chosen either by one of the `set endian big` and `set endian little` commands or by inferring from the last executable used. If no endianness has been previously chosen, then the default for this mode is inferred from the target [GDB] has been built for, and is `little` if the name of the target CPU has an `el` suffix and `big` otherwise.

Note that these commands merely adjust interpretation of symbolic data on the host, and that they have absolutely no effect on the target system.
