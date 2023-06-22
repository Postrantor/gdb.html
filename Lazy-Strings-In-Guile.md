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

A `<gdb:lazy-string>` is represented in [GDB] when printing. A `<gdb:lazy-string>` is retrieved and encoded during printing, while a `<gdb:value>` wrapping a string is immediately retrieved and encoded on creation.

The following lazy-string-related procedures are provided by the `(gdb)` module:

Scheme Procedure: **lazy-string?** *object*

:   Return `#t` if `object` is an object of type `<gdb:lazy-string>`. Otherwise return `#f`.

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

```
<!-- -->
```

Scheme Procedure: **lazy-string-encoding** *lazy-string*

:   Return the encoding that will be applied to `lazy-string` will select the most appropriate encoding when the string is printed.

```
<!-- -->
```

Scheme Procedure: **lazy-string-type** *lazy-string*

:   Return the type that is represented by `lazy-string`'s type. For a lazy string this is a pointer or array type. To resolve this to the lazy string's character type, use `type-target-type`. See [Types In Guile](Types-In-Guile.html#Types-In-Guile).

```
<!-- -->
```

Scheme Procedure: **lazy-string-\>value** *lazy-string*

:   Convert the `<gdb:lazy-string>` to a `<gdb:value>`. This value will point to the string in memory, but will lose all the delayed retrieval, encoding and handling that [GDB] applies to a `<gdb:lazy-string>`.

---

::: header
Next: [Architectures In Guile](Architectures-In-Guile.html#Architectures-In-Guile)]
:::
