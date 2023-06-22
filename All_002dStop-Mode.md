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

Conversely, whenever you restart the program, *all* threads start executing. *This is true even when single-stepping* with commands like `step` or `next`.

In particular, [GDB]), other threads may execute more than one statement while the current thread completes a single step. Moreover, in general other threads stop in the middle of a statement, rather than at a clean statement boundary, when the program stops.

You might even find your program stopped in another thread after continuing or even single-stepping. This happens whenever some other thread runs into a breakpoint, a signal, or an exception before the first thread completes whatever you requested.

Whenever [GDB]' to identify the thread.

On some OSes, you can modify [GDB]'s default behavior by locking the OS scheduler to allow only a single thread to run.

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

By default, when you issue one of the execution commands such as `continue`, `next` or `step`, [GDB] to allow all threads of all the inferiors to run with the `set schedule-multiple` command.

`set schedule-multiple`

Set the mode for allowing threads of multiple processes to be resumed when an execution command is issued. When `on`, all threads of all processes are allowed to run. When `off`, only the threads of the current process are resumed. The default is `off`. The `scheduler-locking` mode takes precedence when set to `on`, or while you are stepping and set to `step`.

`show schedule-multiple`

Display the current mode for resuming the execution of threads of multiple processes.

---

::: header
Next: [Non-Stop Mode](Non_002dStop-Mode.html#Non_002dStop-Mode)]
:::
