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

There are two types of tags that are used in this setup: logical and allocation. A logical tag is stored in the pointers themselves, usually at the higher bits of the pointers. An allocation tag is the tag associated with particular ranges of memory in the physical address space, against which the logical tags from pointers are compared.

The pointer tag (logical tag) must match the memory tag (allocation tag) for the memory access to be valid. If the logical tag does not match the allocation tag, that will raise a memory violation.

Allocation tags cover multiple contiguous bytes of physical memory. This range of bytes is called a memory tag granule and is architecture-specific. For example, AArch64 has a tag granule of 16 bytes, meaning each allocation tag spans 16 bytes of memory.

If the underlying architecture supports memory tagging, like AArch64 MTE or SPARC ADI do, [GDB] can make use of it to validate pointers against memory allocation tags.

The `print` (see [Data](Data.html#Data)) and `x` (see [Memory](Memory.html#Memory)) commands will display tag information when appropriate, and a command prefix of `memory-tag` gives access to the various memory tagging commands.

The `memory-tag` commands are the following:

`memory-tag print-logical-tag pointer_expression`

Print the logical tag stored in `pointer_expression`

`memory-tag with-logical-tag pointer_expression tag_bytes`

Print the pointer given by `pointer_expression`

`memory-tag print-allocation-tag address_expression`

Print the allocation tag associated with the memory address given by `address_expression`

`memory-tag setatag starting_address length tag_bytes`

Set the allocation tag(s) for memory range [\

`memory-tag check pointer_expression`

Check if the logical tag in the pointer given by `pointer_expression` matches the allocation tag for the memory referenced by the pointer.

This essentially emulates the hardware validation that is done when tagged memory is accessed through a pointer, but does not cause a memory fault as it would during hardware validation.

It can be used to inspect potential memory tagging violations in the running process, before any faults get triggered.

---

::: header
Next: [Auto Display](Auto-Display.html#Auto-Display)]
:::
