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

`^Z^Zframes-invalid`

The frames (for example, output from the `backtrace` command) may have changed.

`^Z^Zbreakpoints-invalid`

The breakpoints may have changed. For example, the user just added or deleted a breakpoint.
