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
