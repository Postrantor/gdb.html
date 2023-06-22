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
