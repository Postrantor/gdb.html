---
tip: translate by openai@2023-06-23 18:41:20
...
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

> 默认情况下，GDB允许某些非标准转换，例如将整数常量提升为指针。


Range checking, if turned on, is done on mathematical operations. Array indices are not checked, since they are often used to index a pointer that is not itself an array.

> 如果打开范围检查功能，则会对数学运算进行检查。不检查数组索引，因为它们通常用于索引不是数组的指针。
