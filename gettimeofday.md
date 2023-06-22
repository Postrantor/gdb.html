---
description: gettimeofday (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: gettimeofday (Debugging with GDB)
lang: en
resource-type: document
title: gettimeofday (Debugging with GDB)
---
::: header
Next: [isatty](isatty.html#isatty)]
:::

---

#### gettimeofday

Synopsis:

:   ::: smallexample
``smallexample int gettimeofday(struct timeval *tv, void *tz);``
:::

Request:

:   '`Fgettimeofday,tvptr,tzptr`'

Return value:

:   On success, 0 is returned, -1 otherwise.

Errors:

:

```
`EINVAL`

:   `tz` is a non-NULL pointer.

`EFAULT`

:   `tvptr` is an invalid pointer value.
```
