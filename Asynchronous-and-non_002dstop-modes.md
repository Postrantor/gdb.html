---
tip: translate by openai@2023-06-23 17:37:11
...
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

> 在某些目标上，GDB能够在目标运行时处理MI命令。这被称为*异步命令执行*（请参见[后台执行](Background-Execution.html#Background-Execution)）。前端可以通过发出`-gdb-set mi-async 1`命令来指定异步执行的偏好，这个命令应在运行可执行文件或附加到目标之前发出。在前端开始运行可执行文件或附加到目标之后，它可以使用`-list-target-features`命令查看是否启用了异步执行。

`-gdb-set mi-async [on|off]`


Set whether MI is in asynchronous mode.

> 设置MI是否处于异步模式。


When `off`, which is the default, MI execution commands (e.g., `-exec-continue`) are foreground commands, and [GDB] waits for the program to stop before processing further commands.

> 当默认的关闭（off）时，MI执行命令（例如`-exec-continue`）是前台命令，[GDB]在程序停止前等待处理更多命令。


When `on`, MI execution commands are background execution commands (e.g., `-exec-continue` becomes the equivalent of the `c&` CLI command), and so [GDB] is capable of processing MI commands even while the target is running.

> 当MI处于开启状态时，MI执行的命令是后台执行命令（例如，`-exec-continue`等价于CLI命令`c&`），因此[GDB]能够在目标运行时处理MI命令。

`-gdb-show mi-async`


Show whether MI asynchronous mode is enabled.

> 检查MI异步模式是否已启用。

Note: In [GDB] version 7.7 and earlier, this option was called `target-async` instead of `mi-async`, and it had the effect of both putting MI in asynchronous mode and making CLI background commands possible. CLI background commands are now always possible "out of the box" if the target supports them. The old spelling is kept as a deprecated alias for backwards compatibility.


Even if [GDB] can accept a command while target is running, many commands that access the target do not work when the target is running. Therefore, asynchronous command execution is most useful when combined with non-stop mode (see [Non-Stop Mode](Non_002dStop-Mode.html#Non_002dStop-Mode)). Then, it is possible to examine the state of one thread, while other threads are running.

> 即使GDB可以在目标运行时接受命令，许多访问目标的命令在目标运行时也无法工作。因此，异步命令执行最有用的时候是与非停止模式结合使用（参见非停止模式）。这样，就可以在其他线程运行时检查一个线程的状态。


When a given thread is running, MI commands that try to access the target in the context of that thread may not work, or may work only on some targets. In particular, commands that try to operate on thread's stack will not work, on any target. Commands that read memory, or modify breakpoints, may work or not work, depending on the target. Note that even commands that operate on global state, such as `print`, `set`, and breakpoint commands, still access the target in the context of a specific thread, so frontend should try to find a stopped thread and perform the operation on that thread (using the '`--thread`' option).

> 当一个特定的线程正在运行时，试图在该线程上下文中访问目标的MI命令可能无法工作，或者只能在某些目标上工作。特别是，试图操作线程堆栈的命令将不会在任何目标上工作。读取内存或修改断点的命令可能会根据目标而有不同的效果。请注意，即使是操作全局状态的命令（如“print”、“set”和断点命令）仍然是在特定线程的上下文中访问目标，因此前端应该尝试找到一个已停止的线程并在该线程上执行操作（使用“--thread”选项）。


Which commands will work in the context of a running thread is highly target dependent. However, the two commands `-exec-interrupt`, to stop a thread, and `-thread-info`, to find the state of a thread, will always work.

> 在运行线程的上下文中，哪些命令可以工作是高度依赖于目标的。但是， `-exec-interrupt` 命令，用于停止线程，和 `-thread-info` 命令，用于查找线程状态，将始终有效。

---

::: header
Next: [Thread groups](Thread-groups.html#Thread-groups)]
:::
