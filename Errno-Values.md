---
tip: translate by openai@2023-06-23 20:52:12
...
---
description: Errno Values (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Errno Values (Debugging with GDB)
lang: en
resource-type: document
title: Errno Values (Debugging with GDB)
---
::: header
Next: [Lseek Flags](Lseek-Flags.html#Lseek-Flags)]
:::

---

#### Errno Values

All values are given in decimal representation.

::: smallexample

```bash
  EPERM           1
  ENOENT          2
  EINTR           4
  EBADF           9
  EACCES         13
  EFAULT         14
  EBUSY          16
  EEXIST         17
  ENODEV         19
  ENOTDIR        20
  EISDIR         21
  EINVAL         22
  ENFILE         23
  EMFILE         24
  EFBIG          27
  ENOSPC         28
  ESPIPE         29
  EROFS          30
  ENAMETOOLONG   91
  EUNKNOWN       9999
```

:::

`EUNKNOWN` is used as a fallback error value if a host system returns any error value not in the list of supported error numbers.
