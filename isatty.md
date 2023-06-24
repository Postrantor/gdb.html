---
tip: translate by openai@2023-06-23 23:42:47
...
---
description: isatty (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: isatty (Debugging with GDB)
lang: en
resource-type: document
title: isatty (Debugging with GDB)
---
::: header
Next: [system](system.html#system)]
:::

---

#### isatty

Synopsis:

:   ::: smallexample
``smallexample int isatty(int fd);``
:::

Request:

:   '`Fisatty,fd`'

Return value:

:   Returns 1 if `fd` console, 0 otherwise.

Errors:

:

```
`EINTR`

:   The call was interrupted by the user.
```


Note that the `isatty` call is treated as a special case: it returns 1 to the target if the file descriptor is attached to the [GDB] console, 0 otherwise. Implementing through system calls would require implementing `ioctl` and would be more complex than needed.

> 注意，`isatty`调用被视为一种特殊情况：如果文件描述符附加到[GDB]控制台，则该调用将向目标返回1，否则返回0。通过系统调用实现将需要实现`ioctl`，并且比所需的更复杂。
