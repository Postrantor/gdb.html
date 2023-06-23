---
description: Value Sizes (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Value Sizes (Debugging with GDB)
lang: en
resource-type: document
title: Value Sizes (Debugging with GDB)
---
::: header
Previous: [Searching Memory](Searching-Memory.html#Searching-Memory)]
:::

---

### 10.24 Value Sizes

Whenever [GDB] to try and allocate an overly large amount of memory.

`set max-value-size bytes`

`set max-value-size unlimited`

Set the maximum size of memory that [GDB], trying to display a value that requires more memory than that will result in an error.

Setting this variable does not effect values that have already been allocated within [GDB], only future allocations.

There's a minimum size that `max-value-size` can be set to in order that [GDB] can still operate correctly, this minimum is currently 16 bytes.

The limit applies to the results of some subexpressions as well as to complete expressions. For example, an expression denoting a simple integer component, such as `x.y.z`, may fail if the size of `x.y`.

The default value of `max-value-size` is currently 64k.

`show max-value-size`

Show the maximum size of memory, in bytes, that [GDB] will allocate for the contents of a value.
