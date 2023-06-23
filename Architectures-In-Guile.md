---
description: Architectures In Guile (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Architectures In Guile (Debugging with GDB)
lang: en
resource-type: document
title: Architectures In Guile (Debugging with GDB)
---
::: header
Next: [Disassembly In Guile](Disassembly-In-Guile.html#Disassembly-In-Guile)]
:::

---

#### 23.4.3.21 Guile representation of architectures

[GDB] uses architecture specific parameters and artifacts in a number of its various computations. An architecture is represented by an instance of the `<gdb:arch>` class.

The following architecture-related procedures are provided by the `(gdb)` module:

Scheme Procedure: **arch?** *object*

:   Return `#t` if `object` is an object of type `<gdb:arch>`. Otherwise return `#f`.

```
<!-- -->
```

Scheme Procedure: **current-arch**

:   Return the current architecture as a `<gdb:arch>` object.

```
<!-- -->
```

Scheme Procedure: **arch-name** *arch*

:   Return the name (string value) of `<gdb:arch>` `arch`.

```
<!-- -->
```

Scheme Procedure: **arch-charset** *arch*

:   Return name of target character set of `<gdb:arch>` `arch`.

```
<!-- -->
```

Scheme Procedure: **arch-wide-charset**

:   Return name of target wide character set of `<gdb:arch>` `arch`.

Each architecture provides a set of predefined types, obtained by the following functions.

Scheme Procedure: **arch-void-type** *arch*

:   Return the `<gdb:type>` object for a `void` type of architecture `arch`.

```
<!-- -->
```

Scheme Procedure: **arch-char-type** *arch*

:   Return the `<gdb:type>` object for a `char` type of architecture `arch`.

```
<!-- -->
```

Scheme Procedure: **arch-short-type** *arch*

:   Return the `<gdb:type>` object for a `short` type of architecture `arch`.

```
<!-- -->
```

Scheme Procedure: **arch-int-type** *arch*

:   Return the `<gdb:type>` object for an `int` type of architecture `arch`.

```
<!-- -->
```

Scheme Procedure: **arch-long-type** *arch*

:   Return the `<gdb:type>` object for a `long` type of architecture `arch`.

```
<!-- -->
```

Scheme Procedure: **arch-schar-type** *arch*

:   Return the `<gdb:type>` object for a `signed char` type of architecture `arch`.

```
<!-- -->
```

Scheme Procedure: **arch-uchar-type** *arch*

:   Return the `<gdb:type>` object for an `unsigned char` type of architecture `arch`.

```
<!-- -->
```

Scheme Procedure: **arch-ushort-type** *arch*

:   Return the `<gdb:type>` object for an `unsigned short` type of architecture `arch`.

```
<!-- -->
```

Scheme Procedure: **arch-uint-type** *arch*

:   Return the `<gdb:type>` object for an `unsigned int` type of architecture `arch`.

```
<!-- -->
```

Scheme Procedure: **arch-ulong-type** *arch*

:   Return the `<gdb:type>` object for an `unsigned long` type of architecture `arch`.

```
<!-- -->
```

Scheme Procedure: **arch-float-type** *arch*

:   Return the `<gdb:type>` object for a `float` type of architecture `arch`.

```
<!-- -->
```

Scheme Procedure: **arch-double-type** *arch*

:   Return the `<gdb:type>` object for a `double` type of architecture `arch`.

```
<!-- -->
```

Scheme Procedure: **arch-longdouble-type** *arch*

:   Return the `<gdb:type>` object for a `long double` type of architecture `arch`.

```
<!-- -->
```

Scheme Procedure: **arch-bool-type** *arch*

:   Return the `<gdb:type>` object for a `bool` type of architecture `arch`.

```
<!-- -->
```

Scheme Procedure: **arch-longlong-type** *arch*

:   Return the `<gdb:type>` object for a `long long` type of architecture `arch`.

```
<!-- -->
```

Scheme Procedure: **arch-ulonglong-type** *arch*

:   Return the `<gdb:type>` object for an `unsigned long long` type of architecture `arch`.

```
<!-- -->
```

Scheme Procedure: **arch-int8-type** *arch*

:   Return the `<gdb:type>` object for an `int8` type of architecture `arch`.

```
<!-- -->
```

Scheme Procedure: **arch-uint8-type** *arch*

:   Return the `<gdb:type>` object for a `uint8` type of architecture `arch`.

```
<!-- -->
```

Scheme Procedure: **arch-int16-type** *arch*

:   Return the `<gdb:type>` object for an `int16` type of architecture `arch`.

```
<!-- -->
```

Scheme Procedure: **arch-uint16-type** *arch*

:   Return the `<gdb:type>` object for a `uint16` type of architecture `arch`.

```
<!-- -->
```

Scheme Procedure: **arch-int32-type** *arch*

:   Return the `<gdb:type>` object for an `int32` type of architecture `arch`.

```
<!-- -->
```

Scheme Procedure: **arch-uint32-type** *arch*

:   Return the `<gdb:type>` object for a `uint32` type of architecture `arch`.

```
<!-- -->
```

Scheme Procedure: **arch-int64-type** *arch*

:   Return the `<gdb:type>` object for an `int64` type of architecture `arch`.

```
<!-- -->
```

Scheme Procedure: **arch-uint64-type** *arch*

:   Return the `<gdb:type>` object for a `uint64` type of architecture `arch`.

Example:

::: smallexample

```bash
(gdb) guile (type-name (arch-uchar-type (current-arch)))
"unsigned char"
```

:::

---

::: header
Next: [Disassembly In Guile](Disassembly-In-Guile.html#Disassembly-In-Guile)]
:::
