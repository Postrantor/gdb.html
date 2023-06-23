---
tip: translate by openai@2023-06-23 14:13:10
...
---
description: system (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: system (Debugging with GDB)
lang: en
resource-type: document
title: system (Debugging with GDB)
----------------------------------

::: header
Previous: [isatty](isatty.html#isatty)]
:::

---

#### system

Synopsis:

:   ::: smallexample
``smallexample int system(const char *command);``
:::

Request:

:   '`Fsystem,commandptr/len`'

> 系统，命令指针/长度

Return value:

:   If `len` could not be executed, 127 is returned.

> 如果无法执行 `len`，则返回 127。

Errors:

:

```
`EINTR`

:   The call was interrupted by the user.
```

[GDB] takes over the full task of calling the necessary host calls to perform the `system` call. The return value of `system` on the host is simplified before it's returned to the target. Any termination signal information from the child process is discarded, and the return value consists entirely of the exit status of the called command.

> GDB 负责调用执行 `system` 调用所需的所有主机调用。主机上的 `system` 返回值在返回给目标之前简化。子进程的任何终止信号信息都会被丢弃，返回值完全由调用命令的退出状态组成。

Due to security concerns, the `system` call is by default refused by [GDB]. The user has to allow this call explicitly with the `set remote system-call-allowed 1` command.

> 由于安全原因，[GDB]默认拒绝 `system` 调用。用户必须使用 `set remote system-call-allowed 1` 命令明确允许此调用。

`set remote system-call-allowed`

:

```
Control whether to allow the `system` calls in the File I/O protocol for the remote target. The default is zero (disabled).
```

`show remote system-call-allowed`

:

```
Show whether the `system` calls are allowed in the File I/O protocol.
```
