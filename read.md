---
tip: translate by openai@2023-06-24 01:51:53
...
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

> 如果成功，将返回读取的字节数。零表示文件结束。如果计数为零，也会返回零。如果出错，则返回-1。

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
