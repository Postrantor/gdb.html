---
tip: translate by openai@2023-06-23 19:00:21
...
---
description: close (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: close (Debugging with GDB)
lang: en
resource-type: document
title: close (Debugging with GDB)
---
::: header
Next: [read](read.html#read)]
:::

---

#### close

Synopsis:

:   ::: smallexample
``smallexample int close(int fd);``
:::

Request:

:   '`Fclose,fd`'

Return value:


:   `close` returns zero on success, or -1 if an error occurred.

> 关闭成功时会返回 0，如果发生错误则返回 -1。

Errors:

:

```
`EBADF`

:   `fd` isn't a valid open file descriptor.

`EINTR`

:   The call was interrupted by the user.
```
