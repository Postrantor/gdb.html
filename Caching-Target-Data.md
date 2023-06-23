---
description: Caching Target Data (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Caching Target Data (Debugging with GDB)
lang: en
resource-type: document
title: Caching Target Data (Debugging with GDB)
---
::: header
Next: [Searching Memory](Searching-Memory.html#Searching-Memory)]
:::

---

### 10.22 Caching Data of Targets

[GDB] or in the code segment. Other regions of memory can be explicitly marked as cacheable; see [Memory Region Attributes](Memory-Region-Attributes.html#Memory-Region-Attributes).

`set remotecache on`

`set remotecache off`

This option no longer does anything; it exists for compatibility with old scripts.

`show remotecache`

Show the current state of the obsolete remotecache flag.

`set stack-cache on`

`set stack-cache off`

Enable or disable caching of stack accesses. When `on`, use caching. By default, this option is `on`.

`show stack-cache`

Show the current state of data caching for memory accesses.

`set code-cache on`

`set code-cache off`

Enable or disable caching of code segment accesses. When `on`, use caching. By default, this option is `on`. This improves performance of disassembly in remote debugging.

`show code-cache`

Show the current state of target memory cache for code segment accesses.

`info dcache [line]`

Print the information about the performance of data cache of the current inferior's address space. The information displayed includes the dcache width and depth, and for each cache line, its number, address, and how many times it was referenced. This command is useful for debugging the data cache operation.

If a line number is specified, the contents of that line will be printed in hex.

`set dcache size size`

Set maximum number of entries in dcache (dcache depth above).

`set dcache line-size line-size`

Set number of bytes each dcache entry caches (dcache width above). Must be a power of 2.

`show dcache size`

Show maximum number of dcache entries. See [info dcache](#Caching-Target-Data).

`show dcache line-size`

Show default size of dcache lines.

`maint flush dcache`

Flush the contents (if any) of the dcache. This maintainer command is useful when debugging the dcache implementation.

::: footnote

---

#### Footnotes

### [(13)](#DOCF13)

In non-stop mode, it is moderately rare for a running thread to modify the stack of a stopped thread in a way that would interfere with a backtrace, and caching of stack reads provides a significant speed up of remote backtraces.
:::

---

::: header
Next: [Searching Memory](Searching-Memory.html#Searching-Memory)]
:::
