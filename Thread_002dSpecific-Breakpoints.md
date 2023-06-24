---
tip: translate by openai@2023-06-24 04:03:06
...
---
description: Thread-Specific Breakpoints (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Thread-Specific Breakpoints (Debugging with GDB)
lang: en
resource-type: document
title: Thread-Specific Breakpoints (Debugging with GDB)
---
::: header
Next: [Interrupted System Calls](Interrupted-System-Calls.html#Interrupted-System-Calls)]
:::

---

#### 5.5.4 Thread-Specific Breakpoints


When your program has multiple threads (see [Debugging Programs with Multiple Threads](Threads.html#Threads)), you can choose whether to set breakpoints on all threads, or on a particular thread.

> 当你的程序有多个线程（参见[调试多线程程序](Threads.html#Threads)）时，你可以选择是在所有线程上设置断点，还是只在特定的线程上设置断点。

`break locspec thread thread-id`

`break locspec thread thread-id if …`

`locspec` specifies a code location or locations in your program. See [Location Specifications](Location-Specifications.html#Location-Specifications), for details.

Use the qualifier '`thread thread-id`' display.


If you do not specify '`thread thread-id`' when you set a breakpoint, the breakpoint applies to *all* threads of your program.

> 如果你在设置断点时没有指定'thread thread-id'，那么断点将适用于程序的所有线程。


You can use the `thread` qualifier on conditional breakpoints as well; in this case, place '`thread thread-id`' before or after the breakpoint condition, like this:

> 你也可以在条件断点上使用'thread'限定符；在这种情况下，将 'thread thread-id' 放在断点条件之前或之后，如下所示：

::: smallexample

```bash
(gdb) break frik.c:13 thread 28 if bartab > lim
```

:::


Thread-specific breakpoints are automatically deleted when [GDB] detects the corresponding thread is no longer in the thread list. For example:

> 线程特定断点会在[GDB]检测到相应的线程不再存在于线程列表时自动删除。例如：

::: smallexample

```bash
(gdb) c
Thread-specific breakpoint 3 deleted - thread 28 no longer in the thread list.
```

:::


There are several ways for a thread to disappear, such as a regular thread exit, but also when you detach from the process with the `detach` command (see [Debugging an Already-running Process](Attach.html#Attach)), or if [GDB] is only able to detect a thread has exited when the user explictly asks for the thread list with the `info threads` command.

> 有几种方式可以让线程消失，比如正常的线程退出，也可以使用`detach`命令从进程中分离（参见[调试已运行的进程](Attach.html#Attach)），或者如果[GDB]只能在用户明确要求查看线程列表时，才能检测到线程已退出，使用`info threads`命令时。

---

::: header
Next: [Interrupted System Calls](Interrupted-System-Calls.html#Interrupted-System-Calls)]
:::
