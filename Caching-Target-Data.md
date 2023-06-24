---
tip: translate by openai@2023-06-23 18:47:50
...
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

> [GDB] 或者在代码段中。其他内存区域可以显式标记为可缓存；参见[内存区域属性](Memory-Region-Attributes.html#Memory-Region-Attributes)。

`set remotecache on`

`set remotecache off`


This option no longer does anything; it exists for compatibility with old scripts.

> 这个选项不再有任何作用；它只是为了与旧脚本兼容而存在。

`show remotecache`


Show the current state of the obsolete remotecache flag.

> 显示过时的remotecache标志的当前状态。

`set stack-cache on`

`set stack-cache off`


Enable or disable caching of stack accesses. When `on`, use caching. By default, this option is `on`.

> 启用或禁用堆栈访问的缓存。当“开启”时，使用缓存。默认情况下，此选项为“开启”。

`show stack-cache`


Show the current state of data caching for memory accesses.

> 显示内存访问的数据缓存的当前状态。

`set code-cache on`

`set code-cache off`


Enable or disable caching of code segment accesses. When `on`, use caching. By default, this option is `on`. This improves performance of disassembly in remote debugging.

> 启用或禁用代码段访问的缓存。当“开启”时，使用缓存。默认情况下，此选项为“开启”。这可以提高远程调试中反汇编的性能。

`show code-cache`


Show the current state of target memory cache for code segment accesses.

> 显示代码段访问的目标内存缓存的当前状态。

`info dcache [line]`


Print the information about the performance of data cache of the current inferior's address space. The information displayed includes the dcache width and depth, and for each cache line, its number, address, and how many times it was referenced. This command is useful for debugging the data cache operation.

> 打印当前下级地址空间的数据缓存性能的信息。显示的信息包括dcache的宽度和深度，以及每个缓存行的编号、地址和被引用的次数。这个命令对于调试数据缓存操作很有用。


If a line number is specified, the contents of that line will be printed in hex.

> 如果指定了行号，该行的内容将以十六进制形式打印出来。

`set dcache size size`


Set maximum number of entries in dcache (dcache depth above).

> 设置dcache中的最大条目数（上面的dcache深度）。

`set dcache line-size line-size`


Set number of bytes each dcache entry caches (dcache width above). Must be a power of 2.

> 设置每个dcache条目缓存的字节数（上面的dcache宽度）。必须是2的幂。

`show dcache size`


Show maximum number of dcache entries. See [info dcache](#Caching-Target-Data).

> 查看最大的dcache条目数。参见[info dcache](#Caching-Target-Data)。

`show dcache line-size`


Show default size of dcache lines.

> 显示dcache行的默认大小。

`maint flush dcache`


Flush the contents (if any) of the dcache. This maintainer command is useful when debugging the dcache implementation.

> 清除dcache的内容（如果有的话）。当调试dcache实现时，此维护命令非常有用。

::: footnote

---

#### Footnotes

### [(13)](#DOCF13)


In non-stop mode, it is moderately rare for a running thread to modify the stack of a stopped thread in a way that would interfere with a backtrace, and caching of stack reads provides a significant speed up of remote backtraces.

> 在非停止模式下，运行线程修改停止线程的堆栈以影响回溯的情况相对罕见，而且缓存堆栈读取可以显著加快远程回溯的速度。
:::

---

::: header
Next: [Searching Memory](Searching-Memory.html#Searching-Memory)]
:::
