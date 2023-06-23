---
description: Non-Stop Mode (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Non-Stop Mode (Debugging with GDB)
lang: en
resource-type: document
title: Non-Stop Mode (Debugging with GDB)
---
::: header
Next: [Background Execution](Background-Execution.html#Background-Execution)]
:::

---

#### 5.5.2 Non-Stop Mode

For some multi-threaded targets, [GDB] supports an optional mode of operation in which you can examine stopped program threads in the debugger while other threads continue to execute freely. This minimizes intrusion when debugging live systems, such as programs where some threads have real-time constraints or must continue to respond to external events. This is referred to as *non-stop* mode.

In non-stop mode, when a thread stops to report a debugging event, *only* that thread is stopped; [GDB] does not stop other threads as well, in contrast to the all-stop mode behavior. Additionally, execution commands such as `continue` and `step` apply by default only to the current thread in non-stop mode, rather than all threads as in all-stop mode. This allows you to control threads explicitly in ways that are not possible in all-stop mode --- for example, stepping one thread while allowing others to run freely, stepping one thread while holding all others stopped, or stepping several threads independently and simultaneously.

To enter non-stop mode, use this sequence of commands before you run or attach to your program:

::: smallexample

```bash
# If using the CLI, pagination breaks non-stop.
set pagination off

# Finally, turn it on!
set non-stop on
```

:::

You can use these commands to manipulate the non-stop mode setting:

`set non-stop on`

Enable selection of non-stop mode.

`set non-stop off`

Disable selection of non-stop mode.

`show non-stop`

Show the current non-stop enablement setting.

Note these commands only reflect whether non-stop mode is enabled, not whether the currently-executing program is being run in non-stop mode. In particular, the `set non-stop` preference is only consulted when [GDB] may still fall back to all-stop operation by default.

In non-stop mode, all execution commands apply only to the current thread by default. That is, `continue` only continues one thread. To continue all threads, issue `continue -a` or `c -a`.

You can use [GDB]. The MI execution commands (see [GDB/MI Program Execution](GDB_002fMI-Program-Execution.html#GDB_002fMI-Program-Execution)) are always executed asynchronously in non-stop mode.

Suspending execution is done with the `interrupt` command when running in the background, or [Ctrl-c] during foreground execution. In all-stop mode, this stops the whole process; but in non-stop mode the interrupt applies only to the current thread. To stop the whole program, use `interrupt -a`.

Other execution commands do not currently support the `-a` option.

In non-stop mode, when a thread stops, [GDB] unexpectedly changed to a different thread just as you entered a command to operate on the previously current thread.

---

::: header
Next: [Background Execution](Background-Execution.html#Background-Execution)]
:::
