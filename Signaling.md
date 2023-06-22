---
description: Signaling (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Signaling (Debugging with GDB)
lang: en
resource-type: document
title: Signaling (Debugging with GDB)
---
::: header
Next: [Returning](Returning.html#Returning)]
:::

---

### 17.3 Giving your Program a Signal

`signal signal`

Resume execution where your program is stopped, but immediately give it the signal `signal` can be the name or the number of a signal. For example, on many systems `signal 2` and `signal SIGINT` are both ways of sending an interrupt signal.

Alternatively, if `signal`' causes it to resume without a signal.

*Note:* When resuming a multi-threaded program, `signal` detects that and asks for confirmation.

Invoking the `signal` command is not the same as invoking the `kill` utility from the shell. Sending a signal with `kill` causes [GDB] to decide what to do with the signal depending on the signal handling tables (see [Signals](Signals.html#Signals)). The `signal` command passes the signal directly to your program.

`signal` does not repeat when you press RET a second time after executing the command.

`queue-signal signal`

Queue `signal` with the `handle` command (see [Signals](Signals.html#Signals)).

Alternatively, if `signal` is zero, any currently queued signal for the current thread is discarded and when execution resumes no signal will be delivered. This is useful when your program stopped on account of a signal and would ordinarily see the signal when resumed with the `continue` command.

This command differs from the `signal` command in that the signal is just queued, execution is not resumed. And `queue-signal` cannot be used to pass a signal whose handling state has been set to `nopass` (see [Signals](Signals.html#Signals)).

See [stepping into signal handlers](Signals.html#stepping-into-signal-handlers), for information on how stepping commands behave when the thread has a signal queued.

---

::: header
Next: [Returning](Returning.html#Returning)]
:::
