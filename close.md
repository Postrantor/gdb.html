---
description: close (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: close (Debugging with GDB)
lang: en
resource-type: document
title: close (Debugging with GDB)
---
::: header
Next: [read](read.html#read)]
:::

---

#### close

Synopsis:

:   ::: smallexample
``smallexample int close(int fd);``
:::

Request:

:   '`Fclose,fd`'

Return value:

:   `close` returns zero on success, or -1 if an error occurred.

Errors:

:

```
`EBADF`

:   `fd` isn't a valid open file descriptor.

`EINTR`

:   The call was interrupted by the user.
```
