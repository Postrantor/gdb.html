---
description: isatty (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: isatty (Debugging with GDB)
lang: en
resource-type: document
title: isatty (Debugging with GDB)
---
::: header
Next: [system](system.html#system)]
:::

---

#### isatty

Synopsis:

:   ::: smallexample
``smallexample int isatty(int fd);``
:::

Request:

:   '`Fisatty,fd`'

Return value:

:   Returns 1 if `fd` console, 0 otherwise.

Errors:

:

```
`EINTR`

:   The call was interrupted by the user.
```

Note that the `isatty` call is treated as a special case: it returns 1 to the target if the file descriptor is attached to the [GDB] console, 0 otherwise. Implementing through system calls would require implementing `ioctl` and would be more complex than needed.
