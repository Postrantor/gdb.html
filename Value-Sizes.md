---
tip: translate by openai@2023-06-23 15:23:44
...
---
description: Value Sizes (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Value Sizes (Debugging with GDB)
lang: en
resource-type: document
title: Value Sizes (Debugging with GDB)
---------------------------------------

::: header
Previous: [Searching Memory](Searching-Memory.html#Searching-Memory)]
:::

---

### 10.24 Value Sizes

Whenever [GDB] to try and allocate an overly large amount of memory.

> 每当 GDB 试图分配过大的内存量时。

`set max-value-size bytes`

`set max-value-size unlimited`

Set the maximum size of memory that [GDB], trying to display a value that requires more memory than that will result in an error.

> GDB 设置最大内存大小，如果尝试显示需要更多内存的值，将会导致错误。

Setting this variable does not effect values that have already been allocated within [GDB], only future allocations.

> 设置这个变量不会影响[GDB]中已分配的值，只会影响未来的分配。

There's a minimum size that `max-value-size` can be set to in order that [GDB] can still operate correctly, this minimum is currently 16 bytes.

> 在 GDB 能够正常运行的情况下，`max-value-size` 设置的最小值为 16 字节。

The limit applies to the results of some subexpressions as well as to complete expressions. For example, an expression denoting a simple integer component, such as `x.y.z`, may fail if the size of `x.y`.

> 限制也适用于某些子表达式的结果以及完整表达式。例如，表示简单整数组件的表达式，如 `x.y.z`，如果 `x.y` 的大小失败，则可能会失败。

The default value of `max-value-size` is currently 64k.

> 默认的 `max-value-size` 的值目前为 64k。

`show max-value-size`

Show the maximum size of memory, in bytes, that [GDB] will allocate for the contents of a value.

> GDB 最多可分配多少字节的内存用于存储值的内容？
