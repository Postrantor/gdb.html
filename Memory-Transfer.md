---
tip: translate by openai@2023-06-24 00:17:24
...
---
description: Memory Transfer (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Memory Transfer (Debugging with GDB)
lang: en
resource-type: document
title: Memory Transfer (Debugging with GDB)
---
::: header
Next: [struct stat](struct-stat.html#struct-stat)]
:::

---

#### Memory Transfer


Structured data which is transferred using a memory read or write (for example, a `struct stat`) is expected to be in a protocol-specific format with all scalar multibyte datatypes being big endian. Translation to this representation needs to be done both by the target before the `F` packet is sent, and by [GDB] before it transfers memory to the target. Transferred pointers to structured data should point to the already-coerced data at any time.

> 经过内存读写传输的结构化数据（例如`struct stat`）预期必须以协议特定的格式存在，其中所有标量多字节数据类型都是大端模式。在发送`F`包之前，目标需要进行转换，[GDB]也需要在将内存传输给目标之前进行转换。传输的指向结构数据的指针应该始终指向已经转换的数据。
