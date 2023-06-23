---
tip: translate by openai@2023-06-23 15:44:23
...
---
description: write (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: write (Debugging with GDB)
lang: en
resource-type: document
title: write (Debugging with GDB)
---------------------------------

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

> 写入，fd，bufptr，计数

Return value:

:   On success, the number of bytes written are returned. Zero indicates nothing was written. On error, -1 is returned.

> 如果成功，将返回写入的字节数。零表示没有写入。如果出错，则返回-1。

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
