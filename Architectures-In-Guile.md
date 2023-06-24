---
tip: translate by openai@2023-06-23 17:19:22
...
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

> GDB在其各种计算中使用了特定于架构的参数和工件。架构由<gdb:arch>类的实例表示。


The following architecture-related procedures are provided by the `(gdb)` module:

> `(gdb)` 模块提供以下与架构相关的程序：


Scheme Procedure: **arch?** *object*

> 方案程序：**arch？** *物体*


:   Return `#t` if `object` is an object of type `<gdb:arch>`. Otherwise return `#f`.

> 如果对象是<gdb:arch>类型的对象，则返回#t。否则返回#f。

```
<!-- -->
```


Scheme Procedure: **current-arch**

> 方案程序：**当前架构**


:   Return the current architecture as a `<gdb:arch>` object.

> 返回当前架构作为`<gdb:arch>`对象。

```
<!-- -->
```


Scheme Procedure: **arch-name** *arch*

> 方案程序：** arch-name ** * arch *


:   Return the name (string value) of `<gdb:arch>` `arch`.

> 返回<gdb:arch>的名称（字符串值）的arch。

```
<!-- -->
```


Scheme Procedure: **arch-charset** *arch*

> 方案程序：** arch-charset ** * arch *


:   Return name of target character set of `<gdb:arch>` `arch`.

> 返回`<gdb:arch>` `arch`的目标字符集的名称。

```
<!-- -->
```


Scheme Procedure: **arch-wide-charset**

> 方案程序：**arch-wide-charset**


:   Return name of target wide character set of `<gdb:arch>` `arch`.

> 返回<gdb:arch> arch的目标宽字符集的名称。


Each architecture provides a set of predefined types, obtained by the following functions.

> 每种架构都提供一组通过以下函数获得的预定义类型。


Scheme Procedure: **arch-void-type** *arch*

> 方案程序：**arch-void-type** *arch*


:   Return the `<gdb:type>` object for a `void` type of architecture `arch`.

> 返回架构`arch`的`void`类型的`<gdb:type>`对象。

```
<!-- -->
```


Scheme Procedure: **arch-char-type** *arch*

> 方案程序：**arch-char-type** *arch*

架构字符类型：*arch*


:   Return the `<gdb:type>` object for a `char` type of architecture `arch`.

> 返回适用于架构`arch`的`char`类型的`<gdb:type>`对象。

```
<!-- -->
```


Scheme Procedure: **arch-short-type** *arch*

> 方案程序：** arch-short-type ** * arch *


:   Return the `<gdb:type>` object for a `short` type of architecture `arch`.

> 返回架构arch的短类型的<gdb:type>对象。

```
<!-- -->
```


Scheme Procedure: **arch-int-type** *arch*

> 方案程序：** arch-int-type ** * arch *


:   Return the `<gdb:type>` object for an `int` type of architecture `arch`.

> 返回`arch`架构的`int`类型的`<gdb:type>`对象。

```
<!-- -->
```


Scheme Procedure: **arch-long-type** *arch*

> 方案程序：**arch-long-type** *arch*


:   Return the `<gdb:type>` object for a `long` type of architecture `arch`.

> 返回架构`arch`的`long`类型的`<gdb:type>`对象。

```
<!-- -->
```


Scheme Procedure: **arch-schar-type** *arch*

> 方案程序：** arch-schar-type** * arch*


:   Return the `<gdb:type>` object for a `signed char` type of architecture `arch`.

> 返回架构`arch`的`signed char`类型的`<gdb:type>`对象。

```
<!-- -->
```


Scheme Procedure: **arch-uchar-type** *arch*

> 方案程序：**arch-uchar-type** *arch*


:   Return the `<gdb:type>` object for an `unsigned char` type of architecture `arch`.

> 返回`arch`架构的`unsigned char`类型的`<gdb:type>`对象。

```
<!-- -->
```


Scheme Procedure: **arch-ushort-type** *arch*

> 方案程序：**arch-ushort-type** *arch*


:   Return the `<gdb:type>` object for an `unsigned short` type of architecture `arch`.

> 返回架构`arch`上`unsigned short`类型的`<gdb:type>`对象。

```
<!-- -->
```


Scheme Procedure: **arch-uint-type** *arch*

> 方案程序：**arch-uint-type** *arch*


:   Return the `<gdb:type>` object for an `unsigned int` type of architecture `arch`.

> 返回`<gdb:type>`对象，该对象用于架构`arch`的无符号整型类型。

```
<!-- -->
```


Scheme Procedure: **arch-ulong-type** *arch*

> 方案程序：** arch-ulong-type ** * arch *


:   Return the `<gdb:type>` object for an `unsigned long` type of architecture `arch`.

> 返回架构`arch`的`unsigned long`类型的`<gdb:type>`对象。

```
<!-- -->
```


Scheme Procedure: **arch-float-type** *arch*

> 方案程序：**arch-float-type** *arch*


:   Return the `<gdb:type>` object for a `float` type of architecture `arch`.

> 返回`arch`架构的`float`类型的`<gdb:type>`对象

```
<!-- -->
```


Scheme Procedure: **arch-double-type** *arch*

> 方案程序：** arch-double-type ** * arch *


:   Return the `<gdb:type>` object for a `double` type of architecture `arch`.

> 返回`arch`架构的`double`类型的`<gdb:type>`对象。

```
<!-- -->
```


Scheme Procedure: **arch-longdouble-type** *arch*

> 方案程序：**arch-longdouble-type** *arch*


:   Return the `<gdb:type>` object for a `long double` type of architecture `arch`.

> 返回`arch`架构的`long double`类型的`<gdb:type>`对象。

```
<!-- -->
```


Scheme Procedure: **arch-bool-type** *arch*

> 方案程序：**arch-bool-type** *arch*


:   Return the `<gdb:type>` object for a `bool` type of architecture `arch`.

> 返回`arch`架构的`bool`类型的`<gdb:type>`对象。

```
<!-- -->
```


Scheme Procedure: **arch-longlong-type** *arch*

> 方案程序：**arch-longlong-type** *arch*


:   Return the `<gdb:type>` object for a `long long` type of architecture `arch`.

> 返回架构`arch`的`long long`类型的`<gdb:type>`对象。

```
<!-- -->
```


Scheme Procedure: **arch-ulonglong-type** *arch*

> 方案程序：**arch-ulonglong-type** *arch*


:   Return the `<gdb:type>` object for an `unsigned long long` type of architecture `arch`.

> 返回架构`arch`上`unsigned long long`类型的`<gdb:type>`对象。

```
<!-- -->
```


Scheme Procedure: **arch-int8-type** *arch*

> 方案程序：**arch-int8-type** *arch*


:   Return the `<gdb:type>` object for an `int8` type of architecture `arch`.

> 返回`arch`架构的`int8`类型的`<gdb:type>`对象。

```
<!-- -->
```


Scheme Procedure: **arch-uint8-type** *arch*

> 方案程序：**arch-uint8-type** *arch*


:   Return the `<gdb:type>` object for a `uint8` type of architecture `arch`.

> 返回`arch`上`uint8`类型的`<gdb:type>`对象。

```
<!-- -->
```


Scheme Procedure: **arch-int16-type** *arch*

> 方案程序：**arch-int16-type** *arch*


:   Return the `<gdb:type>` object for an `int16` type of architecture `arch`.

> 返回架构`arch`的`int16`类型的`<gdb:type>`对象。

```
<!-- -->
```


Scheme Procedure: **arch-uint16-type** *arch*

> 方案程序：** arch-uint16-type ** * arch *


:   Return the `<gdb:type>` object for a `uint16` type of architecture `arch`.

> 返回`arch`架构的`uint16`类型的`<gdb:type>`对象。

```
<!-- -->
```


Scheme Procedure: **arch-int32-type** *arch*

> 方案程序：** arch-int32-type ** * arch *


:   Return the `<gdb:type>` object for an `int32` type of architecture `arch`.

> 返回`arch`架构中`int32`类型的`<gdb:type>`对象。

```
<!-- -->
```


Scheme Procedure: **arch-uint32-type** *arch*

> 方案程序：** arch-uint32-type ** * arch *


:   Return the `<gdb:type>` object for a `uint32` type of architecture `arch`.

> 返回架构`arch`的`uint32`类型的`<gdb:type>`对象。

```
<!-- -->
```


Scheme Procedure: **arch-int64-type** *arch*

> 方案程序：**arch-int64-type** *arch*


:   Return the `<gdb:type>` object for an `int64` type of architecture `arch`.

> 返回'arch'架构的int64类型的'<gdb:type>'对象。

```
<!-- -->
```


Scheme Procedure: **arch-uint64-type** *arch*

> 方案程序：** arch-uint64-type ** * arch *


:   Return the `<gdb:type>` object for a `uint64` type of architecture `arch`.

> 返回<gdb:type>对象，它是架构arch上的uint64类型。

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
