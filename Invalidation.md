---
tip: translate by openai@2023-06-23 23:35:46
...
---
description: Invalidation (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Invalidation (Debugging with GDB)
lang: en
resource-type: document
title: Invalidation (Debugging with GDB)
---
::: header
Next: [Annotations for Running](Annotations-for-Running.html#Annotations-for-Running)]
:::

---

### 28.5 Invalidation Notices


The following annotations say that certain pieces of state may have changed.

> 以下注释表明某些状态可能已经改变。

`^Z^Zframes-invalid`


The frames (for example, output from the `backtrace` command) may have changed.

> 框架（例如，来自`backtrace`命令的输出）可能已经改变。

`^Z^Zbreakpoints-invalid`


The breakpoints may have changed. For example, the user just added or deleted a breakpoint.

> 断点可能已经改变了。例如，用户刚刚添加或删除了断点。
