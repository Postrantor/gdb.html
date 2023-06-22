---
description: Console I/O (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Console I/O (Debugging with GDB)
lang: en
resource-type: document
title: Console I/O (Debugging with GDB)
---
::: header
Next: [List of Supported Calls](List-of-Supported-Calls.html#List-of-Supported-Calls)]
:::

---

#### E.13.6 Console I/O

By default and if not explicitly closed by the target system, the file descriptors 0, 1 and 2 are connected to the [GDB] so that after the target read request from file descriptor 0 all following typing is buffered until either one of the following conditions is met:

- The user types [Ctrl-c]. The behaviour is as explained above, and the `read` system call is treated as finished.
- The user presses RET. This is treated as end of input with a trailing newline.
- The user types [Ctrl-d]') is appended to the input.

If the user has typed more characters than fit in the buffer given to the `read` call, the trailing characters are buffered in [GDB] until either another `read(0, …)` is requested by the target, or debugging is stopped at the user's request.
