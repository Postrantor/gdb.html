---
tip: translate by openai@2023-06-23 17:26:53
...
---
description: Arithmetic In Guile (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Arithmetic In Guile (Debugging with GDB)
lang: en
resource-type: document
title: Arithmetic In Guile (Debugging with GDB)
---
::: header
Next: [Types In Guile](Types-In-Guile.html#Types-In-Guile)]
:::

---

#### 23.4.3.6 Arithmetic In Guile


The `(gdb)` module provides several functions for performing arithmetic on `<gdb:value>` objects. The arithmetic is performed as if it were done by the target, and therefore has target semantics which are not necessarily those of Scheme. For example operations work with a fixed precision, not the arbitrary precision of Scheme.

> 模块(gdb)提供了一些函数，用于对<gdb:value>对象执行算术运算。算术运算的执行方式就像是由目标执行的一样，因此具有目标语义，这些语义不一定是Scheme的语义。例如，操作使用固定精度，而不是Scheme的任意精度。


Wherever a function takes an integer or pointer as an operand, [GDB] will convert appropriate Scheme values to perform the operation.

> 无论函数将整数或指针作为操作数，[GDB]都会将适当的Scheme值转换为执行操作。


Scheme Procedure: **value-add** *a b*

> 方案程序：**value-add** *a b*


Scheme Procedure: **value-sub** *a b*

> 方案步骤：**value-sub** *a b*


Scheme Procedure: **value-mul** *a b*

> 方案程序：**value-mul** *a b*


Scheme Procedure: **value-div** *a b*

> 方案程序：**value-div** *a b*


Scheme Procedure: **value-rem** *a b*

> 方案程序：**value-rem** *a b*


Scheme Procedure: **value-mod** *a b*

> 方案程序：**value-mod** *a b*


Scheme Procedure: **value-pow** *a b*

> 方案程序：**value-pow** *a b*


Scheme Procedure: **value-not** *a*

> 方案程序：**value-not** *a*


Scheme Procedure: **value-neg** *a*

> 方案程序：**value-neg** *a*


Scheme Procedure: **value-pos** *a*

> 方案程序：**value-pos** *a*


Scheme Procedure: **value-abs** *a*

> 方案程序：**value-abs** *a*


Scheme Procedure: **value-lsh** *a b*

> 方案程序：**value-lsh** *a b*


Scheme Procedure: **value-rsh** *a b*

> 方案程序：**value-rsh** *a b*


Scheme Procedure: **value-min** *a b*

> 方案程序：**value-min** *a b*


Scheme Procedure: **value-max** *a b*

> 方案程序：**value-max** *a b*


Scheme Procedure: **value-lognot** *a*

> 方案程序：**value-lognot** *a*


Scheme Procedure: **value-logand** *a b*

> 方案程序：**value-logand** *a b*


Scheme Procedure: **value-logior** *a b*

> 方案步骤：**value-logior** *a b*


Scheme Procedure: **value-logxor** *a b*

> 方案程序：**value-logxor** *a b*


Scheme Procedure: **value=?** *a b*

> 方案程序：**值=？** *a b*


Scheme Procedure: **value\<?** *a b*

> 方案程序：**值？** *a b*


Scheme Procedure: **value\<=?** *a b*

> 方案程序：**value\<=?** *a b*


Scheme Procedure: **value\>?** *a b*

> 方案程序：**值>？** *a b*


Scheme Procedure: **value\>=?** *a b*

> 方案程序：**值> =？** * a b *


Scheme does not provide a `not-equal` function, and thus Guile support in [GDB] does not either.

> 方案不提供“不等于”函数，因此[GDB]中的Guile支持也没有。

---

::: header
Next: [Types In Guile](Types-In-Guile.html#Types-In-Guile)]
:::
