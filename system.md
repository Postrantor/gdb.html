---
description: system (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: system (Debugging with GDB)
lang: en
resource-type: document
title: system (Debugging with GDB)
---
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

Return value:

:   If `len` could not be executed, 127 is returned.

Errors:

:

```
`EINTR`

:   The call was interrupted by the user.
```

[GDB] takes over the full task of calling the necessary host calls to perform the `system` call. The return value of `system` on the host is simplified before it's returned to the target. Any termination signal information from the child process is discarded, and the return value consists entirely of the exit status of the called command.

Due to security concerns, the `system` call is by default refused by [GDB]. The user has to allow this call explicitly with the `set remote system-call-allowed 1` command.

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
