---
tip: translate by openai@2023-06-24 03:01:48
...
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

> 在`文件名`后跟一个或多个小写十六进制数字（注意，这与语言无关）。
