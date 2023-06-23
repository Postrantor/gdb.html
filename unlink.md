---
tip: translate by openai@2023-06-23 15:15:47
...
---
description: unlink (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: unlink (Debugging with GDB)
lang: en
resource-type: document
title: unlink (Debugging with GDB)
----------------------------------

::: header
Next: [stat/fstat](stat_002ffstat.html#stat_002ffstat)]
:::

---

#### unlink

Synopsis:

:   ::: smallexample
``smallexample int unlink(const char *pathname);``
:::

Request:

:   '`Funlink,pathnameptr/len`'

> Funlink，pathnameptr/len

Return value:

:   On success, zero is returned. On error, -1 is returned.

> 在成功的情况下，返回零。在出错的情况下，返回-1。

Errors:

:

```
`EACCES`

:   No access to the file or the path of the file.

`EPERM`

:   The system does not allow unlinking of directories.

`EBUSY`

:   The file `pathname` cannot be unlinked because it's being used by another process.

`EFAULT`

:   `pathnameptr` is an invalid pointer value.

`ENAMETOOLONG`

:   `pathname` was too long.

`ENOENT`

:   A directory component in `pathname` does not exist.

`ENOTDIR`

:   A component of the path is not a directory.

`EROFS`

:   The file is on a read-only filesystem.

`EINTR`

:   The call was interrupted by the user.
```
