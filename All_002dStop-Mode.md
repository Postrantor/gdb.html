---
tip: translate by openai@2023-06-23 17:09:03
...
---
description: All-Stop Mode (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: All-Stop Mode (Debugging with GDB)
lang: en
resource-type: document
title: All-Stop Mode (Debugging with GDB)
---
::: header
Next: [Non-Stop Mode](Non_002dStop-Mode.html#Non_002dStop-Mode)]
:::

---

#### 5.5.1 All-Stop Mode


In all-stop mode, whenever your program stops under [GDB] for any reason, *all* threads of execution stop, not just the current thread. This allows you to examine the overall state of the program, including switching between threads, without worrying that things may change underfoot.

> 在全停止模式下，无论你的程序在[GDB]中因为任何原因而停止，*所有*的执行线程都会停止，而不仅仅是当前线程。这样可以让你检查程序的整体状态，包括在线程之间切换，而不用担心情况会发生变化。


Conversely, whenever you restart the program, *all* threads start executing. *This is true even when single-stepping* with commands like `step` or `next`.

> 反之，每次你重新启动程序时，所有线程都会开始执行。即使使用`步进`或`下一步`等命令单步执行，也是如此。


In particular, [GDB]), other threads may execute more than one statement while the current thread completes a single step. Moreover, in general other threads stop in the middle of a statement, rather than at a clean statement boundary, when the program stops.

> 特别是，其他线程在当前线程完成单步操作时可以执行多条语句。此外，一般情况下，当程序停止时，其他线程会在语句中间而不是在干净的语句边界处停止。


You might even find your program stopped in another thread after continuing or even single-stepping. This happens whenever some other thread runs into a breakpoint, a signal, or an exception before the first thread completes whatever you requested.

> 你甚至可能在继续或单步执行之后，发现你的程序在另一个线程中停止了。只要其他线程在第一个线程完成你请求的操作之前遇到断点、信号或异常，就会发生这种情况。


Whenever [GDB]' to identify the thread.

> 每当[GDB]时，用以识别线程。


On some OSes, you can modify [GDB]'s default behavior by locking the OS scheduler to allow only a single thread to run.

> 在某些操作系统上，您可以通过锁定操作系统调度程序来允许只运行一个线程，以修改GDB的默认行为。

`set scheduler-locking mode`

:

```
Set the scheduler locking mode. It applies to normal execution, record mode, and replay mode. `mode` can be one of the following:

`off`

:   There is no locking and any thread may run at any time.

`on`

:   Only the current thread may run when the inferior is resumed.

`step`

:   Behaves like `on` when stepping, and `off` otherwise. Threads other than the current never get a chance to run when you step, and they are completely free to run when you use commands like '`continue`'.

    This mode optimizes for single-stepping; it prevents other threads from preempting the current thread while you are stepping, so that the focus of debugging does not change unexpectedly. However, unless another thread hits a breakpoint during its timeslice, [GDB] does not change the current thread away from the thread that you are debugging.

`replay`

:   Behaves like `on` in replay mode, and `off` in either record mode or during normal execution. This is the default mode.
```

`show scheduler-locking`


:   Display the current scheduler locking mode.

> 显示当前调度程序锁定模式。


By default, when you issue one of the execution commands such as `continue`, `next` or `step`, [GDB] to allow all threads of all the inferiors to run with the `set schedule-multiple` command.

> 默认情况下，当你发出一个执行命令，如`continue`，`next`或`step`时，[GDB]会使用`set schedule-multiple`命令允许所有下属线程运行。

`set schedule-multiple`


Set the mode for allowing threads of multiple processes to be resumed when an execution command is issued. When `on`, all threads of all processes are allowed to run. When `off`, only the threads of the current process are resumed. The default is `off`. The `scheduler-locking` mode takes precedence when set to `on`, or while you are stepping and set to `step`.

> 设置允许多个进程的线程在发出执行命令时恢复的模式。当设置为“on”时，所有进程的所有线程都允许运行。当设置为“off”时，只有当前进程的线程才会恢复。默认为“off”。当设置为“on”或者在设置为“step”时步进时，调度器锁定模式优先。

`show schedule-multiple`


Display the current mode for resuming the execution of threads of multiple processes.

> 显示多个进程线程恢复执行的当前模式。

---

::: header
Next: [Non-Stop Mode](Non_002dStop-Mode.html#Non_002dStop-Mode)]
:::
