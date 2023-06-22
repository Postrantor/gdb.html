---
description: Pascal (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Pascal (Debugging with GDB)
lang: en
resource-type: document
title: Pascal (Debugging with GDB)
---
::: header
Next: [Rust](Rust.html#Rust)]
:::

---

#### 15.4.7 Pascal

Debugging Pascal programs which use sets, subranges, file variables, or nested functions does not currently work. [GDB] does not support entering expressions, printing values, or similar features using Pascal syntax.

The Pascal-specific command `set print pascal_static-members` controls whether static members of Pascal objects are displayed. See [pascal_static-members](Print-Settings.html#Print-Settings).
