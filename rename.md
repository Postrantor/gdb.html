---
description: rename (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: rename (Debugging with GDB)
lang: en
resource-type: document
title: rename (Debugging with GDB)
---
::: header
Next: [unlink](unlink.html#unlink)]
:::

---

#### rename

Synopsis:

:   ::: smallexample
``smallexample int rename(const char *oldpath, const char *newpath);``
:::

Request:

:   '`Frename,oldpathptr/len,newpathptr/len`'

Return value:

:   On success, zero is returned. On error, -1 is returned.

Errors:

:

```
`EISDIR`

:   `newpath` is not a directory.

`EEXIST`

:   `newpath` is a non-empty directory.

`EBUSY`

:   `oldpath` is a directory that is in use by some process.

`EINVAL`

:   An attempt was made to make a directory a subdirectory of itself.

`ENOTDIR`

:   A component used as a directory in `oldpath` exists but is not a directory.

`EFAULT`

:   `oldpathptr` are invalid pointer values.

`EACCES`

:   No access to the file or the path of the file.

`ENAMETOOLONG`

:   `oldpath` was too long.

`ENOENT`

:   A directory component in `oldpath` does not exist.

`EROFS`

:   The file is on a read-only filesystem.

`ENOSPC`

:   The device containing the file has no room for the new directory entry.

`EINTR`

:   The call was interrupted by the user.
```
