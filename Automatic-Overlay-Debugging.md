---
tip: translate by openai@2023-06-23 17:41:42
...
---
description: Automatic Overlay Debugging (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Automatic Overlay Debugging (Debugging with GDB)
lang: en
resource-type: document
title: Automatic Overlay Debugging (Debugging with GDB)
---
::: header
Next: [Overlay Sample Program](Overlay-Sample-Program.html#Overlay-Sample-Program)]
:::

---

### 14.3 Automatic Overlay Debugging


[GDB] looks in the inferior's memory for certain variables describing the current state of the overlays.

> [GDB] 在下层内存中查找描述覆盖当前状态的特定变量。


Here are the variables your overlay manager must define to support [GDB]'s automatic overlay debugging:

> 这些变量是您的覆盖管理器必须定义的，以支持[GDB]的自动覆盖调试：

`_ovly_table`:


:   This variable must be an array of the following structures:

> 这个变量必须是以下结构的数组：

```
::: smallexample
``` smallexample
struct
{

  /* The overlay's mapped address.  */

> /* 覆盖的映射地址。 */
  unsigned long vma;


  /* The size of the overlay, in bytes.  */

> /* 覆盖层的大小，以字节为单位。 */
  unsigned long size;


  /* The overlay's load address.  */

> /* 覆盖的加载地址。 */
  unsigned long lma;


  /* Non-zero if the overlay is currently mapped;

> 如果当前已经映射了叠加层，则非零。
     zero otherwise.  */
  unsigned long mapped;
}
```

:::

```

`_novlys`:


:   This variable must be a four-byte signed integer, holding the total number of elements in `_ovly_table`.

> 这个变量必须是一个4字节的有符号整数，用于存储_ovly_table中的元素总数。


To decide whether a particular overlay is mapped or not, [GDB] finds a matching entry, it consults the entry's `mapped` member to determine whether the overlay is currently mapped.

> 要判断某个特定的覆盖是否映射，[GDB]会找到一个匹配的条目，它会查看该条目的“mapped”成员来确定该覆盖当前是否已映射。


In addition, your overlay manager may define a function called `_ovly_debug_event`. If this function is defined, [GDB] to accurately keep track of which overlays are in program memory, and update any breakpoints that may be set in overlays. This will allow breakpoints to work even if the overlays are kept in ROM or other non-writable memory while they are not being executed.

> 此外，您的覆盖管理器可能会定义一个名为`_ovly_debug_event`的函数。如果定义了此函数，[GDB]将准确跟踪哪些覆盖物位于程序存储器中，并更新可能在覆盖物中设置的任何断点。即使覆盖物在未执行时保留在ROM或其他不可写入的存储器中，这也将允许断点正常工作。

---

::: header
Next: [Overlay Sample Program](Overlay-Sample-Program.html#Overlay-Sample-Program)]
:::
```
