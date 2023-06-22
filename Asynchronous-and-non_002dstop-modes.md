---
description: Asynchronous and non-stop modes (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Asynchronous and non-stop modes (Debugging with GDB)
lang: en
resource-type: document
title: Asynchronous and non-stop modes (Debugging with GDB)
---
::: header
Next: [Thread groups](Thread-groups.html#Thread-groups)]
:::

---

#### 27.1.2 Asynchronous command execution and non-stop mode

On some targets, [GDB] is capable of processing MI commands even while the target is running. This is called *asynchronous command execution* (see [Background Execution](Background-Execution.html#Background-Execution)). The frontend may specify a preference for asynchronous execution using the `-gdb-set mi-async 1` command, which should be emitted before either running the executable or attaching to the target. After the frontend has started the executable or attached to the target, it can find if asynchronous execution is enabled using the `-list-target-features` command.

`-gdb-set mi-async [on|off]`

Set whether MI is in asynchronous mode.

When `off`, which is the default, MI execution commands (e.g., `-exec-continue`) are foreground commands, and [GDB] waits for the program to stop before processing further commands.

When `on`, MI execution commands are background execution commands (e.g., `-exec-continue` becomes the equivalent of the `c&` CLI command), and so [GDB] is capable of processing MI commands even while the target is running.

`-gdb-show mi-async`

Show whether MI asynchronous mode is enabled.

Note: In [GDB] version 7.7 and earlier, this option was called `target-async` instead of `mi-async`, and it had the effect of both putting MI in asynchronous mode and making CLI background commands possible. CLI background commands are now always possible "out of the box" if the target supports them. The old spelling is kept as a deprecated alias for backwards compatibility.

Even if [GDB] can accept a command while target is running, many commands that access the target do not work when the target is running. Therefore, asynchronous command execution is most useful when combined with non-stop mode (see [Non-Stop Mode](Non_002dStop-Mode.html#Non_002dStop-Mode)). Then, it is possible to examine the state of one thread, while other threads are running.

When a given thread is running, MI commands that try to access the target in the context of that thread may not work, or may work only on some targets. In particular, commands that try to operate on thread's stack will not work, on any target. Commands that read memory, or modify breakpoints, may work or not work, depending on the target. Note that even commands that operate on global state, such as `print`, `set`, and breakpoint commands, still access the target in the context of a specific thread, so frontend should try to find a stopped thread and perform the operation on that thread (using the '`--thread`' option).

Which commands will work in the context of a running thread is highly target dependent. However, the two commands `-exec-interrupt`, to stop a thread, and `-thread-info`, to find the state of a thread, will always work.

---

::: header
Next: [Thread groups](Thread-groups.html#Thread-groups)]
:::
