---
description: C Checks (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: C Checks (Debugging with GDB)
lang: en
resource-type: document
title: C Checks (Debugging with GDB)
---
::: header
Next: [Debugging C](Debugging-C.html#Debugging-C)]
:::

---

#### 15.4.1.5 C and C++ Type and Range Checks

By default, when [GDB] will allow certain non-standard conversions, such as promoting integer constants to pointers.

Range checking, if turned on, is done on mathematical operations. Array indices are not checked, since they are often used to index a pointer that is not itself an array.
