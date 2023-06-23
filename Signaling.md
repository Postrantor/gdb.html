---
tip: translate by openai@2023-06-23 13:15:58
...
---
description: Signaling (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Signaling (Debugging with GDB)
lang: en
resource-type: document
title: Signaling (Debugging with GDB)
-------------------------------------

::: header
Next: [Returning](Returning.html#Returning)]
:::

---

### 17.3 Giving your Program a Signal

`signal signal`

Resume execution where your program is stopped, but immediately give it the signal `signal` can be the name or the number of a signal. For example, on many systems `signal 2` and `signal SIGINT` are both ways of sending an interrupt signal.

> 恢复程序的执行，但立即发送信号 `signal`，可以是信号的名称或编号。例如，在许多系统上，`信号2` 和 `信号SIGINT` 都是发送中断信号的方式。

Alternatively, if `signal`' causes it to resume without a signal.

> 另外，如果没有信号，`signal` 可以使其恢复运行。

*Note:* When resuming a multi-threaded program, `signal` detects that and asks for confirmation.

> *注意：* 恢复多线程程序时，`信号` 会检测到并请求确认。

Invoking the `signal` command is not the same as invoking the `kill` utility from the shell. Sending a signal with `kill` causes [GDB] to decide what to do with the signal depending on the signal handling tables (see [Signals](Signals.html#Signals)). The `signal` command passes the signal directly to your program.

> 调用 `signal` 命令与从 shell 中调用 `kill` 工具不同。使用 `kill` 发送信号会导致[GDB]根据信号处理表（参见[信号](Signals.html#Signals)）来决定如何处理信号。`signal` 命令会将信号直接发送到您的程序中。

`signal` does not repeat when you press RET a second time after executing the command.

`queue-signal signal`

Queue `signal` with the `handle` command (see [Signals](Signals.html#Signals)).

> 使用 handle 命令（参见信号）排队信号。

Alternatively, if `signal` is zero, any currently queued signal for the current thread is discarded and when execution resumes no signal will be delivered. This is useful when your program stopped on account of a signal and would ordinarily see the signal when resumed with the `continue` command.

> 如果 `信号` 为零，则会丢弃当前线程的任何已排队的信号，当执行恢复时，不会传递任何信号。当您的程序由于信号而停止，并且通常在使用 `继续` 命令恢复时会看到信号时，这是非常有用的。

This command differs from the `signal` command in that the signal is just queued, execution is not resumed. And `queue-signal` cannot be used to pass a signal whose handling state has been set to `nopass` (see [Signals](Signals.html#Signals)).

> 这个命令与 `signal` 命令的不同之处在于，信号只是被排队，而不会恢复执行。而且 `queue-signal` 不能用来传递已被设置为 `nopass` 的信号（参见[信号](Signals.html#Signals)）。

See [stepping into signal handlers](Signals.html#stepping-into-signal-handlers), for information on how stepping commands behave when the thread has a signal queued.

> 请参阅[进入信号处理程序](Signals.html#stepping-into-signal-handlers)，了解当线程有信号排队时，步进命令的行为。

---

::: header
Next: [Returning](Returning.html#Returning)]
:::
