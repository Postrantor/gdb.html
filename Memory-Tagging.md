---
tip: translate by openai@2023-06-24 00:16:14
...
---
description: Memory Tagging (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Memory Tagging (Debugging with GDB)
lang: en
resource-type: document
title: Memory Tagging (Debugging with GDB)
---
::: header
Next: [Auto Display](Auto-Display.html#Auto-Display)]
:::

---

### 10.7 Memory Tagging


Memory tagging is a memory protection technology that uses a pair of tags to validate memory accesses through pointers. The tags are integer values usually comprised of a few bits, depending on the architecture.

> 内存标记是一种内存保护技术，它使用一对标记来验证通过指针进行的内存访问。标记通常是由几位二进制数组成的整数值，具体取决于架构。


There are two types of tags that are used in this setup: logical and allocation. A logical tag is stored in the pointers themselves, usually at the higher bits of the pointers. An allocation tag is the tag associated with particular ranges of memory in the physical address space, against which the logical tags from pointers are compared.

> 在这个设置中使用了两种标签：逻辑标签和分配标签。逻辑标签通常存储在指针的高位中。分配标签是与物理地址空间中的特定范围相关联的标签，用于与指针的逻辑标签进行比较。


The pointer tag (logical tag) must match the memory tag (allocation tag) for the memory access to be valid. If the logical tag does not match the allocation tag, that will raise a memory violation.

> 指针标记（逻辑标记）必须与内存标记（分配标记）相匹配，才能使内存访问有效。如果逻辑标记与分配标记不匹配，将引发内存违规。


Allocation tags cover multiple contiguous bytes of physical memory. This range of bytes is called a memory tag granule and is architecture-specific. For example, AArch64 has a tag granule of 16 bytes, meaning each allocation tag spans 16 bytes of memory.

> 分配标签覆盖多个连续的物理内存字节。这一字节范围称为内存标签粒度，且与架构有关。例如，AArch64具有16字节的标签粒度，意味着每个分配标签跨越16字节的内存。


If the underlying architecture supports memory tagging, like AArch64 MTE or SPARC ADI do, [GDB] can make use of it to validate pointers against memory allocation tags.

> 如果底层架构支持内存标记，比如AArch64 MTE或SPARC ADI，[GDB]可以利用它来验证指针与内存分配标签的有效性。


The `print` (see [Data](Data.html#Data)) and `x` (see [Memory](Memory.html#Memory)) commands will display tag information when appropriate, and a command prefix of `memory-tag` gives access to the various memory tagging commands.

> 打印（参见[数据](Data.html#Data)）和`x`（参见[内存](Memory.html#Memory)）命令在适当的情况下将显示标签信息，`memory-tag`命令前缀可访问各种内存标签命令。

The `memory-tag` commands are the following:

`memory-tag print-logical-tag pointer_expression`

Print the logical tag stored in `pointer_expression`

`memory-tag with-logical-tag pointer_expression tag_bytes`

Print the pointer given by `pointer_expression`

`memory-tag print-allocation-tag address_expression`


Print the allocation tag associated with the memory address given by `address_expression`

> 打印与给定的内存地址（address_expression）相关联的分配标记。

`memory-tag setatag starting_address length tag_bytes`

Set the allocation tag(s) for memory range [\

`memory-tag check pointer_expression`


Check if the logical tag in the pointer given by `pointer_expression` matches the allocation tag for the memory referenced by the pointer.

> 检查由`pointer_expression`给出的指针中的逻辑标签是否与指针所引用的内存的分配标签匹配。


This essentially emulates the hardware validation that is done when tagged memory is accessed through a pointer, but does not cause a memory fault as it would during hardware validation.

> 这本质上模拟了通过指针访问带标记的内存时所进行的硬件验证，但不会导致内存故障，就像硬件验证时一样。


It can be used to inspect potential memory tagging violations in the running process, before any faults get triggered.

> 它可以用来检查正在运行进程中潜在的内存标记违规，在任何故障触发之前。

---

::: header
Next: [Auto Display](Auto-Display.html#Auto-Display)]
:::
