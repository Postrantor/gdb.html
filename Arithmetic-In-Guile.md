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

Wherever a function takes an integer or pointer as an operand, [GDB] will convert appropriate Scheme values to perform the operation.

Scheme Procedure: **value-add** *a b*

Scheme Procedure: **value-sub** *a b*

Scheme Procedure: **value-mul** *a b*

Scheme Procedure: **value-div** *a b*

Scheme Procedure: **value-rem** *a b*

Scheme Procedure: **value-mod** *a b*

Scheme Procedure: **value-pow** *a b*

Scheme Procedure: **value-not** *a*

Scheme Procedure: **value-neg** *a*

Scheme Procedure: **value-pos** *a*

Scheme Procedure: **value-abs** *a*

Scheme Procedure: **value-lsh** *a b*

Scheme Procedure: **value-rsh** *a b*

Scheme Procedure: **value-min** *a b*

Scheme Procedure: **value-max** *a b*

Scheme Procedure: **value-lognot** *a*

Scheme Procedure: **value-logand** *a b*

Scheme Procedure: **value-logior** *a b*

Scheme Procedure: **value-logxor** *a b*

Scheme Procedure: **value=?** *a b*

Scheme Procedure: **value\<?** *a b*

Scheme Procedure: **value\<=?** *a b*

Scheme Procedure: **value\>?** *a b*

Scheme Procedure: **value\>=?** *a b*

Scheme does not provide a `not-equal` function, and thus Guile support in [GDB] does not either.

---

::: header
Next: [Types In Guile](Types-In-Guile.html#Types-In-Guile)]
:::
