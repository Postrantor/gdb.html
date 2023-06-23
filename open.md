---
description: open (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: open (Debugging with GDB)
lang: en
resource-type: document
title: open (Debugging with GDB)
---
::: header
Next: [close](close.html#close)]
:::

---

#### open

Synopsis:

:   ::: smallexample
``smallexample int open(const char *pathname, int flags); int open(const char *pathname, int flags, mode_t mode);``
:::

Request:

:   '`Fopen,pathptr/len,flags,mode`'

```
`flags` is the bitwise `OR` of the following values:

`O_CREAT`

:   If the file does not exist it will be created. The host rules apply as far as file ownership and time stamps are concerned.

`O_EXCL`

:   When used with `O_CREAT`, if the file already exists it is an error and open() fails.

`O_TRUNC`

:   If the file already exists and the open mode allows writing (`O_RDWR` or `O_WRONLY` is given) it will be truncated to zero length.

`O_APPEND`

:   The file is opened in append mode.

`O_RDONLY`

:   The file is opened for reading only.

`O_WRONLY`

:   The file is opened for writing only.

`O_RDWR`

:   The file is opened for reading and writing.

Other bits are silently ignored.

`mode` is the bitwise `OR` of the following values:

`S_IRUSR`

:   User has read permission.

`S_IWUSR`

:   User has write permission.

`S_IRGRP`

:   Group has read permission.

`S_IWGRP`

:   Group has write permission.

`S_IROTH`

:   Others have read permission.

`S_IWOTH`

:   Others have write permission.

Other bits are silently ignored.
```

Return value:

:   `open` returns the new file descriptor or -1 if an error occurred.

Errors:

:

```
`EEXIST`

:   `pathname` already exists and `O_CREAT` and `O_EXCL` were used.

`EISDIR`

:   `pathname` refers to a directory.

`EACCES`

:   The requested access is not allowed.

`ENAMETOOLONG`

:   `pathname` was too long.

`ENOENT`

:   A directory component in `pathname` does not exist.

`ENODEV`

:   `pathname` refers to a device, pipe, named pipe or socket.

`EROFS`

:   `pathname` refers to a file on a read-only filesystem and write access was requested.

`EFAULT`

:   `pathname` is an invalid pointer value.

`ENOSPC`

:   No space on device to create the file.

`EMFILE`

:   The process already has the maximum number of files open.

`ENFILE`

:   The limit on the total number of files open on the system has been reached.

`EINTR`

:   The call was interrupted by the user.
```

---

::: header
Next: [close](close.html#close)]
:::
