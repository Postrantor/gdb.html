---
tip: translate by openai@2023-06-24 00:34:05
...
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

> 对于一些多线程目标，[GDB]支持一种可选的操作模式，在该模式下，您可以在调试器中检查停止的程序线程，而其他线程继续自由执行。这可以最大限度地减少调试实时系统时的侵入，例如一些线程具有实时约束或必须继续响应外部事件的程序。这被称为*非停止*模式。


In non-stop mode, when a thread stops to report a debugging event, *only* that thread is stopped; [GDB] does not stop other threads as well, in contrast to the all-stop mode behavior. Additionally, execution commands such as `continue` and `step` apply by default only to the current thread in non-stop mode, rather than all threads as in all-stop mode. This allows you to control threads explicitly in ways that are not possible in all-stop mode --- for example, stepping one thread while allowing others to run freely, stepping one thread while holding all others stopped, or stepping several threads independently and simultaneously.

> 在非停止模式下，当一个线程停止报告调试事件时，只有该线程被停止；与全停止模式的行为相比，[GDB]不会停止其他线程。此外，默认情况下，在非停止模式下，执行命令（如`continue`和`step`）只适用于当前线程，而不是全停止模式下的所有线程。这样，您可以以在全停止模式下无法实现的方式显式控制线程 --- 例如，让一个线程自由跳步，同时将其他线程保持停止，或者同时独立地跳步多个线程。


To enter non-stop mode, use this sequence of commands before you run or attach to your program:

> 要进入不间断模式，在运行或附加到程序之前使用此命令序列：

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

> 这些命令只反映非停止模式是否启用，而不是当前正在执行的程序是否处于非停止模式。特别是，只有在[GDB]可能仍然默认回退到全停止操作时，才会查阅`set non-stop`偏好设置。


In non-stop mode, all execution commands apply only to the current thread by default. That is, `continue` only continues one thread. To continue all threads, issue `continue -a` or `c -a`.

> 在不间断模式下，所有执行命令默认只适用于当前线程。也就是说，`continue`只会继续一个线程。要继续所有线程，请发出`continue -a`或`c -a`。


You can use [GDB]. The MI execution commands (see [GDB/MI Program Execution](GDB_002fMI-Program-Execution.html#GDB_002fMI-Program-Execution)) are always executed asynchronously in non-stop mode.

> 你可以使用[GDB]。MI执行命令（参见[GDB/MI程序执行](GDB_002fMI-Program-Execution.html#GDB_002fMI-Program-Execution))总是以非停止模式异步执行。


Suspending execution is done with the `interrupt` command when running in the background, or [Ctrl-c] during foreground execution. In all-stop mode, this stops the whole process; but in non-stop mode the interrupt applies only to the current thread. To stop the whole program, use `interrupt -a`.

> 在后台运行时，使用`interrupt`命令可以挂起执行，或者在前台执行时使用[Ctrl-c]。 在全停止模式下，这会停止整个过程；但是在非停止模式下，中断仅适用于当前线程。 要停止整个程序，请使用`interrupt -a`。

Other execution commands do not currently support the `-a` option.


In non-stop mode, when a thread stops, [GDB] unexpectedly changed to a different thread just as you entered a command to operate on the previously current thread.

> 在不停止模式下，当一个线程停止时，GDB就会意外地切换到另一个线程，就像你输入了一条命令来操作之前的当前线程一样。

---

::: header
Next: [Background Execution](Background-Execution.html#Background-Execution)]
:::
