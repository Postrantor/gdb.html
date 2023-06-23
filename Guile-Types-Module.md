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

Usage:

::: smallexample

```bash
(use-modules (gdb types))
```

:::

Scheme Procedure: **get-basic-type** *type*

:   Return `type` with const and volatile qualifiers stripped, and with typedefs and C++ references converted to the underlying type.

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

```

<!-- -->

```

Scheme Procedure: **make-enum-hashtable** *enum-type*

:   Return a Guile hash table produced from `enum-type`. Elements in the hash table are referenced with `hashq-ref`.
```
