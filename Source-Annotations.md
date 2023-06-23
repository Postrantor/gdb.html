---
description: Source Annotations (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Source Annotations (Debugging with GDB)
lang: en
resource-type: document
title: Source Annotations (Debugging with GDB)
---
::: header
Previous: [Annotations for Running](Annotations-for-Running.html#Annotations-for-Running)]
:::

---

### 28.7 Displaying Source

The following annotation is used instead of displaying source code:

::: smallexample

```bash
^Z^Zsource filename:line:character:middle:addr
```

:::

where `filename`' followed by one or more lowercase hex digits (note that this does not depend on the language).
