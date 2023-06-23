---
tip: translate by openai@2023-06-23 13:37:30
...
---
description: stat/fstat (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: stat/fstat (Debugging with GDB)
lang: en
resource-type: document
title: stat/fstat (Debugging with GDB)
---
::: header
Next: [gettimeofday](gettimeofday.html#gettimeofday)]
:::

---

#### stat/fstat

Synopsis:

:   ::: smallexample
``smallexample int stat(const char *pathname, struct stat *buf); int fstat(int fd, struct stat *buf);``
:::

Request:


:   '`Fstat,pathnameptr/len,bufptr`'

> Fstat，pathnameptr / len，bufptr
'`Ffstat,fd,bufptr`'

Return value:


:   On success, zero is returned. On error, -1 is returned.

> 如果成功，返回0。如果出错，返回-1。

Errors:

:

```
`EBADF`

:   `fd` is not a valid open file.

`ENOENT`

:   A directory component in `pathname` does not exist or the path is an empty string.

`ENOTDIR`

:   A component of the path is not a directory.

`EFAULT`

:   `pathnameptr` is an invalid pointer value.

`EACCES`

:   No access to the file or the path of the file.

`ENAMETOOLONG`

:   `pathname` was too long.

`EINTR`

:   The call was interrupted by the user.
```
