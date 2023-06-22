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

A `gdb.LazyString` is represented in [GDB] when printing. A `gdb.LazyString` is retrieved and encoded during printing, while a `gdb.Value` wrapping a string is immediately retrieved and encoded on creation.

A `gdb.LazyString` object has the following functions:

Function: **LazyString.value** *()*

:   Convert the `gdb.LazyString` to a `gdb.Value`. This value will point to the string in memory, but will lose all the delayed retrieval, encoding and handling that [GDB] applies to a `gdb.LazyString`.

```
<!-- -->
```

Variable: **LazyString.address**

:   This attribute holds the address of the string. This attribute is not writable.

```
<!-- -->
```

Variable: **LazyString.length**

:   This attribute holds the length of the string in characters. If the length is -1, then the string will be fetched and encoded up to the first null of appropriate width. This attribute is not writable.

```
<!-- -->
```

Variable: **LazyString.encoding**

:   This attribute holds the encoding that will be applied to the string when the string is printed by [GDB] will select the most appropriate encoding when the string is printed. This attribute is not writable.

```
<!-- -->
```

Variable: **LazyString.type**

:   This attribute holds the type that is represented by the lazy string's type. For a lazy string this is a pointer or array type. To resolve this to the lazy string's character type, use the type's `target` method. See [Types In Python](Types-In-Python.html#Types-In-Python). This attribute is not writable.

---

::: header
Next: [Architectures In Python](Architectures-In-Python.html#Architectures-In-Python)]
:::
