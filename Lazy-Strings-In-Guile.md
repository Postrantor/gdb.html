---
tip: translate by openai@2023-06-23 23:47:25
...
---
description: Lazy Strings In Guile (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Lazy Strings In Guile (Debugging with GDB)
lang: en
resource-type: document
title: Lazy Strings In Guile (Debugging with GDB)
---
::: header
Next: [Architectures In Guile](Architectures-In-Guile.html#Architectures-In-Guile)]
:::

---

#### 23.4.3.20 Guile representation of lazy strings.


A *lazy string* is a string whose contents is not retrieved or encoded until it is needed.

> 一个懒惰字符串是指直到需要时才获取或编码其内容的字符串。


A `<gdb:lazy-string>` is represented in [GDB] when printing. A `<gdb:lazy-string>` is retrieved and encoded during printing, while a `<gdb:value>` wrapping a string is immediately retrieved and encoded on creation.

> 一个<gdb:lazy-string>在[GDB]中打印时会被表示出来。在打印时，<gdb:lazy-string>会被检索并编码，而<gdb:value>包装的字符串会在创建时立即被检索和编码。


The following lazy-string-related procedures are provided by the `(gdb)` module:

> 以下与惰性字符串相关的程序由`(gdb)`模块提供：

Scheme Procedure: **lazy-string?** *object*


:   Return `#t` if `object` is an object of type `<gdb:lazy-string>`. Otherwise return `#f`.

> 如果对象是类型<gdb:lazy-string>的对象，则返回#t。否则返回#f。

```
<!-- -->
```

Scheme Procedure: **lazy-string-address** *lazy-sring*

:   Return the address of `lazy-string`.

```
<!-- -->
```

Scheme Procedure: **lazy-string-length** *lazy-string*


:   Return the length of `lazy-string` in characters. If the length is -1, then the string will be fetched and encoded up to the first null of appropriate width.

> 返回`lazy-string`的长度（以字符为单位）。如果长度为-1，则会获取字符串并按适当宽度编码至第一个空值。

```
<!-- -->
```

Scheme Procedure: **lazy-string-encoding** *lazy-string*


:   Return the encoding that will be applied to `lazy-string` will select the most appropriate encoding when the string is printed.

> 返回将应用于`lazy-string`的编码时，打印字符串时将选择最合适的编码。

```
<!-- -->
```

Scheme Procedure: **lazy-string-type** *lazy-string*


:   Return the type that is represented by `lazy-string`'s type. For a lazy string this is a pointer or array type. To resolve this to the lazy string's character type, use `type-target-type`. See [Types In Guile](Types-In-Guile.html#Types-In-Guile).

> 返回由“懒惰字符串”的类型表示的类型。对于懒惰的字符串，这是一个指针或数组类型。要将其解析为懒惰字符串的字符类型，请使用“type-target-type”。请参阅[Guile中的类型](Types-In-Guile.html#Types-In-Guile)。

```
<!-- -->
```

Scheme Procedure: **lazy-string-\>value** *lazy-string*


:   Convert the `<gdb:lazy-string>` to a `<gdb:value>`. This value will point to the string in memory, but will lose all the delayed retrieval, encoding and handling that [GDB] applies to a `<gdb:lazy-string>`.

> 将`<gdb:lazy-string>`转换为`<gdb:value>`。该值将指向内存中的字符串，但会丢失[GDB]应用于`<gdb:lazy-string>`的所有延迟检索、编码和处理。

---

::: header
Next: [Architectures In Guile](Architectures-In-Guile.html#Architectures-In-Guile)]
:::
