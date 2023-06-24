---
tip: translate by openai@2023-06-23 21:17:59
...
---
description: Fortran Types (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Fortran Types (Debugging with GDB)
lang: en
resource-type: document
title: Fortran Types (Debugging with GDB)
---
::: header
Next: [Fortran Operators](Fortran-Operators.html#Fortran-Operators)]
:::

---

#### 15.4.6.1 Fortran Types


In Fortran the primitive data-types have an associated `KIND` type parameter, written as '`type*kindparam`'. The kind of a type can be retrieved by using the intrinsic function `KIND`, see [Fortran Intrinsics](Fortran-Intrinsics.html#Fortran-Intrinsics).

> 在Fortran中，原始数据类型具有关联的“KIND”类型参数，写为“type*kindparam”。可以通过使用内置函数KIND来检索类型的种类，详见[Fortran Intrinsics]（Fortran-Intrinsics.html#Fortran-Intrinsics）。


Generally, the actual implementation of the `KIND` type parameter is compiler specific. In [GDB] specifies its size in memory --- a Fortran `Integer*4` or `Integer(kind=4)` would be an integer type occupying 4 bytes of memory. An exception to this rule is the `Complex` type for which the kind of the type does not specify its entire size, but the size of each of the two `Real`'s it is composed of. A `Complex*4` would thus consist of two `Real*4` s and occupy 8 bytes of memory.

> 一般来说，`KIND` 类型参数的实际实现是编译器特定的。在[GDB]中指定其在内存中的大小 --- 一个Fortran `Integer*4` 或 `Integer(kind=4)` 将是一个占用4个字节内存的整数类型。对于`Complex`类型，这一规则有一个例外，其类型的种类不指定其整个大小，而是指定它由两个`Real`组成的每个`Real`的大小。因此，`Complex*4` 将由两个`Real*4`组成，占用8个字节的内存。


For every type there is also a default kind associated with it, e.g. `Integer` in [GDB].

> 对于每种类型，都会有一种默认类型与其关联，例如[GDB]中的`Integer`。


Not every kind parameter is valid for every type and in [GDB] the following type kinds are available.

> 不是每种参数都适用于每种类型，而在[GDB]中可用的类型种类有：

`Integer`


:   `Integer*1`, `Integer*2`, `Integer*4`, `Integer*8`, and `Integer` = `Integer*4`.

> 整数*1、整数*2、整数*4、整数*8以及整数=整数*4。

`Logical`


:   `Logical*1`, `Logical*2`, `Logical*4`, `Logical*8`, and `Logical` = `Logical*4`.

> 逻辑*1、逻辑*2、逻辑*4、逻辑*8，以及逻辑=逻辑*4。

`Real`

:   `Real*4`, `Real*8`, `Real*16`, and `Real` = `Real*4`.

`Complex`

:   `Complex*4`, `Complex*8`, `Complex*16`, and `Complex` = `Complex*4`.

---

::: header
Next: [Fortran Operators](Fortran-Operators.html#Fortran-Operators)]
:::
