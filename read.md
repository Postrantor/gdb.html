---
description: read (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: read (Debugging with GDB)
lang: en
resource-type: document
title: read (Debugging with GDB)
---
::: header
Next: [write](write.html#write)]
:::

---

#### read

Synopsis:

:   ::: smallexample
``smallexample int read(int fd, void *buf, unsigned int count);``
:::

Request:

:   '`Fread,fd,bufptr,count`'

Return value:

:   On success, the number of bytes read is returned. Zero indicates end of file. If count is zero, read returns zero as well. On error, -1 is returned.

Errors:

:

```
`EBADF`

:   `fd` is not a valid file descriptor or is not open for reading.

`EFAULT`

:   `bufptr` is an invalid pointer value.

`EINTR`

:   The call was interrupted by the user.
```
