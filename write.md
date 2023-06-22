---
description: write (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: write (Debugging with GDB)
lang: en
resource-type: document
title: write (Debugging with GDB)
---
::: header
Next: [lseek](lseek.html#lseek)]
:::

---

#### write

Synopsis:

:   ::: smallexample
``smallexample int write(int fd, const void *buf, unsigned int count);``
:::

Request:

:   '`Fwrite,fd,bufptr,count`'

Return value:

:   On success, the number of bytes written are returned. Zero indicates nothing was written. On error, -1 is returned.

Errors:

:

```
`EBADF`

:   `fd` is not a valid file descriptor or is not open for writing.

`EFAULT`

:   `bufptr` is an invalid pointer value.

`EFBIG`

:   An attempt was made to write a file that exceeds the host-specific maximum file size allowed.

`ENOSPC`

:   No space on device to write the data.

`EINTR`

:   The call was interrupted by the user.
```
