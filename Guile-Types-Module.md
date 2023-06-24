---
tip: translate by openai@2023-06-23 23:05:00
...
---
description: Guile Types Module (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Guile Types Module (Debugging with GDB)
lang: en
resource-type: document
title: Guile Types Module (Debugging with GDB)
---
::: header
Previous: [Guile Printing Module](Guile-Printing-Module.html#Guile-Printing-Module)]
:::

---

#### 23.4.5.2 Guile Types Module


This module provides a collection of utilities for working with `<gdb:type>` objects.

> 这个模块提供了一系列用于处理<gdb:type>对象的实用程序。

Usage:

::: smallexample

```bash
(use-modules (gdb types))
```

:::

Scheme Procedure: **get-basic-type** *type*


:   Return `type` with const and volatile qualifiers stripped, and with typedefs and C++ references converted to the underlying type.

> 返回去除了const和volatile限定词，并将typedefs和C++引用转换为底层类型的`type`。

```
C++ example:

::: smallexample
``` smallexample
typedef const int const_int;
const_int foo (3);
const_int& foo_ref (foo);
int main () 
```

:::

Then in gdb:

::: smallexample

```bash
(gdb) start
(gdb) guile (use-modules (gdb) (gdb types))
(gdb) guile (define foo-ref (parse-and-eval "foo_ref"))
(gdb) guile (get-basic-type (value-type foo-ref))
int
```

:::

```

```

<!-- -->

```

Scheme Procedure: **type-has-field-deep?** *type field*


:   Return `#t` if `type`. Otherwise return `#f`. This searches baseclasses, whereas `type-has-field?` does not.

> 如果有`type`，则返回`#t`，否则返回`#f`。这个搜索基类，而`type-has-field?`则不会。

```

<!-- -->

```

Scheme Procedure: **make-enum-hashtable** *enum-type*


:   Return a Guile hash table produced from `enum-type`. Elements in the hash table are referenced with `hashq-ref`.

> 返回一个由`enum-type`生成的Guile哈希表。哈希表中的元素使用`hashq-ref`引用。
```
