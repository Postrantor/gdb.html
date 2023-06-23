---
description: The Ctrl-C Message (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: The Ctrl-C Message (Debugging with GDB)
lang: en
resource-type: document
title: The Ctrl-C Message (Debugging with GDB)
---
::: header
Next: [Console I/O](Console-I_002fO.html#Console-I_002fO)]
:::

---

#### E.13.5 The '`Ctrl-C`

If the '`Ctrl-C` with a `T02` packet.

It's important for the target to know in which state the system call was interrupted. There are two possible cases:

- The system call hasn't been performed on the host yet.
- The system call on the host has been finished.

These two states can be distinguished by the target by the value of the returned `errno`. If it's the protocol representation of `EINTR`, the system call hasn't been performed. This is equivalent to the `EINTR` handling on POSIX systems. In any other case, the target may presume that the system call has been finished --- successfully or not --- and should behave as if the break message arrived right after the system call.

[GDB]. This requires sending `M` or `X` packets as necessary. The `F` packet may only be sent when either nothing has happened or the full action has been completed.

---

::: header
Next: [Console I/O](Console-I_002fO.html#Console-I_002fO)]
:::
