---
tip: translate by openai@2023-06-23 23:48:24
...
---
description: Lazy Strings In Python (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Lazy Strings In Python (Debugging with GDB)
lang: en
resource-type: document
title: Lazy Strings In Python (Debugging with GDB)
---
::: header
Next: [Architectures In Python](Architectures-In-Python.html#Architectures-In-Python)]
:::

---

#### 23.3.2.33 Python representation of lazy strings


A *lazy string* is a string whose contents is not retrieved or encoded until it is needed.

> 一个懒惰的字符串是指直到需要时才被检索或编码的字符串。


A `gdb.LazyString` is represented in [GDB] when printing. A `gdb.LazyString` is retrieved and encoded during printing, while a `gdb.Value` wrapping a string is immediately retrieved and encoded on creation.

> 一个`gdb.LazyString`在[GDB]中打印时会被表示出来。在打印时，`gdb.LazyString`会被检索并编码，而包装字符串的`gdb.Value`则会在创建时立即被检索并编码。

A `gdb.LazyString` object has the following functions:

Function: **LazyString.value** *()*


:   Convert the `gdb.LazyString` to a `gdb.Value`. This value will point to the string in memory, but will lose all the delayed retrieval, encoding and handling that [GDB] applies to a `gdb.LazyString`.

> 将`gdb.LazyString`转换为`gdb.Value`。此值将指向内存中的字符串，但会丢失[GDB]应用于`gdb.LazyString`的所有延迟检索、编码和处理。

```
<!-- -->
```

Variable: **LazyString.address**


:   This attribute holds the address of the string. This attribute is not writable.

> 这个属性保存字符串的地址。这个属性是不可写的。

```
<!-- -->
```

Variable: **LazyString.length**


:   This attribute holds the length of the string in characters. If the length is -1, then the string will be fetched and encoded up to the first null of appropriate width. This attribute is not writable.

> 这个属性保存字符串的长度（以字符为单位）。如果长度为-1，则字符串将被获取并编码到适当宽度的第一个空值。这个属性是不可写的。

```
<!-- -->
```

Variable: **LazyString.encoding**


:   This attribute holds the encoding that will be applied to the string when the string is printed by [GDB] will select the most appropriate encoding when the string is printed. This attribute is not writable.

> 此属性保存将在[GDB]打印字符串时应用的编码。打印字符串时，GDB将选择最合适的编码。此属性不可写。

```
<!-- -->
```

Variable: **LazyString.type**


:   This attribute holds the type that is represented by the lazy string's type. For a lazy string this is a pointer or array type. To resolve this to the lazy string's character type, use the type's `target` method. See [Types In Python](Types-In-Python.html#Types-In-Python). This attribute is not writable.

> 这个属性保存了被懒惰字符串所表示的类型。对于懒惰字符串，这是一个指针或数组类型。要将其解析为懒惰字符串的字符类型，请使用该类型的`target`方法。参见[Python中的类型](Types-In-Python.html#Types-In-Python)。此属性不可写。

---

::: header
Next: [Architectures In Python](Architectures-In-Python.html#Architectures-In-Python)]
:::
