---
tip: translate by openai@2023-06-23 14:39:29
...
---
description: Thread-Specific Breakpoints (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Thread-Specific Breakpoints (Debugging with GDB)
lang: en
resource-type: document
title: Thread-Specific Breakpoints (Debugging with GDB)
-------------------------------------------------------

::: header
Next: [Interrupted System Calls](Interrupted-System-Calls.html#Interrupted-System-Calls)]
:::

---

#### 5.5.4 Thread-Specific Breakpoints

When your program has multiple threads (see [Debugging Programs with Multiple Threads](Threads.html#Threads)), you can choose whether to set breakpoints on all threads, or on a particular thread.

> 当您的程序有多个线程（参见[调试多线程程序](Threads.html#Threads)）时，您可以选择是在所有线程上设置断点，还是在特定的线程上设置断点。

`break locspec thread thread-id`

`break locspec thread thread-id if …`

`locspec` specifies a code location or locations in your program. See [Location Specifications](Location-Specifications.html#Location-Specifications), for details.

Use the qualifier '`thread thread-id`' display.

> 使用限定符“thread thread-id”显示。

If you do not specify '`thread thread-id`' when you set a breakpoint, the breakpoint applies to *all* threads of your program.

> 如果你在设置断点时没有指定'thread thread-id'，那么断点将适用于程序的所有线程。

You can use the `thread` qualifier on conditional breakpoints as well; in this case, place '`thread thread-id`' before or after the breakpoint condition, like this:

> 你也可以在条件断点上使用'thread'限定符；在这种情况下，在断点条件之前或之后放置'thread thread-id'，就像这样：

::: smallexample

```bash
(gdb) break frik.c:13 thread 28 if bartab > lim
```

:::

Thread-specific breakpoints are automatically deleted when [GDB] detects the corresponding thread is no longer in the thread list. For example:

> 线程特定断点会在[GDB]检测到相应线程不再存在于线程列表时自动删除。例如：

::: smallexample

```bash
(gdb) c
Thread-specific breakpoint 3 deleted - thread 28 no longer in the thread list.
```

:::

There are several ways for a thread to disappear, such as a regular thread exit, but also when you detach from the process with the `detach` command (see [Debugging an Already-running Process](Attach.html#Attach)), or if [GDB] is only able to detect a thread has exited when the user explictly asks for the thread list with the `info threads` command.

> 有几种方法可以使线程消失，比如定期线程退出，但也可以使用 `detach` 命令（参见[调试正在运行的进程](Attach.html#Attach)）从进程中分离，或者如果[GDB]只能在用户显式要求查看线程列表时使用 `info threads` 命令检测到线程已退出时。

---

::: header
Next: [Interrupted System Calls](Interrupted-System-Calls.html#Interrupted-System-Calls)]
:::
