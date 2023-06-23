---
description: lseek (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: lseek (Debugging with GDB)
lang: en
resource-type: document
title: lseek (Debugging with GDB)
---
::: header
Next: [rename](rename.html#rename)]
:::

---

#### lseek

Synopsis:

:   ::: smallexample
``smallexample long lseek (int fd, long offset, int flag);``
:::

Request:

:   '`Flseek,fd,offset,flag`'

```
`flag` is one of:

`SEEK_SET`

:   The offset is set to `offset` bytes.

`SEEK_CUR`

:   The offset is set to its current location plus `offset` bytes.

`SEEK_END`

:   The offset is set to the size of the file plus `offset` bytes.
```

Return value:

:   On success, the resulting unsigned offset in bytes from the beginning of the file is returned. Otherwise, a value of -1 is returned.

Errors:

:

```
`EBADF`

:   `fd` is not a valid open file descriptor.

`ESPIPE`

:   `fd` console.

`EINVAL`

:   `flag` is not a proper value.

`EINTR`

:   The call was interrupted by the user.
```
