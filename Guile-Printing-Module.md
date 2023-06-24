---
tip: translate by openai@2023-06-23 23:04:53
...
---
description: Guile Printing Module (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Guile Printing Module (Debugging with GDB)
lang: en
resource-type: document
title: Guile Printing Module (Debugging with GDB)
---
::: header
Next: [Guile Types Module](Guile-Types-Module.html#Guile-Types-Module)]
:::

---

#### 23.4.5.1 Guile Printing Module


This module provides a collection of utilities for working with pretty-printers.

> 这个模块提供了一系列用于处理美化打印机的实用程序。

Usage:

::: smallexample

```bash
(use-modules (gdb printing))
```

:::

Scheme Procedure: **prepend-pretty-printer!** *object printer*

:   Add `printer` is added to the global list of printers.

```
<!-- -->
```

Scheme Procecure: **append-pretty-printer!** *object printer*

:   Add `printer` is added to the global list of printers.
