---
tip: translate by openai@2023-06-23 14:26:59
...
---
description: The Ctrl-C Message (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: The Ctrl-C Message (Debugging with GDB)
lang: en
resource-type: document
title: The Ctrl-C Message (Debugging with GDB)
----------------------------------------------

::: header
Next: [Console I/O](Console-I_002fO.html#Console-I_002fO)]
:::

---

#### E.13.5 The '`Ctrl-C`

If the '`Ctrl-C` with a `T02` packet.

> 如果使用 T02 数据包，请按 Ctrl-C。

It's important for the target to know in which state the system call was interrupted. There are two possible cases:

> 重要的是，目标要知道系统调用在何种状态中被中断。有两种可能的情况：

- The system call hasn't been performed on the host yet.
- The system call on the host has been finished.

These two states can be distinguished by the target by the value of the returned `errno`. If it's the protocol representation of `EINTR`, the system call hasn't been performed. This is equivalent to the `EINTR` handling on POSIX systems. In any other case, the target may presume that the system call has been finished --- successfully or not --- and should behave as if the break message arrived right after the system call.

> 这两个状态可以通过返回的 `errno` 的值来被目标区分。如果它是 `EINTR` 的协议表示，则系统调用尚未执行。这相当于 POSIX 系统上的 `EINTR` 处理。在任何其他情况下，目标可以假定系统调用已经完成---无论成功与否---并应该像系统调用之后立即收到中断消息一样行为。

[GDB]. This requires sending `M` or `X` packets as necessary. The `F` packet may only be sent when either nothing has happened or the full action has been completed.

> 需要发送 `M` 或 `X` 数据包。仅当什么也没发生或完成整个操作时，才可以发送 `F` 数据包。

---

::: header
Next: [Console I/O](Console-I_002fO.html#Console-I_002fO)]
:::
