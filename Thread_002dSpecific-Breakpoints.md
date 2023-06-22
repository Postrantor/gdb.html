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

`break locspec thread thread-id`

`break locspec thread thread-id if …`

`locspec` specifies a code location or locations in your program. See [Location Specifications](Location-Specifications.html#Location-Specifications), for details.

Use the qualifier '`thread thread-id`' display.

If you do not specify '`thread thread-id`' when you set a breakpoint, the breakpoint applies to *all* threads of your program.

You can use the `thread` qualifier on conditional breakpoints as well; in this case, place '`thread thread-id`' before or after the breakpoint condition, like this:

::: smallexample

```bash
(gdb) break frik.c:13 thread 28 if bartab > lim
```

:::

Thread-specific breakpoints are automatically deleted when [GDB] detects the corresponding thread is no longer in the thread list. For example:

::: smallexample

```bash
(gdb) c
Thread-specific breakpoint 3 deleted - thread 28 no longer in the thread list.
```

:::

There are several ways for a thread to disappear, such as a regular thread exit, but also when you detach from the process with the `detach` command (see [Debugging an Already-running Process](Attach.html#Attach)), or if [GDB] is only able to detect a thread has exited when the user explictly asks for the thread list with the `info threads` command.

---

::: header
Next: [Interrupted System Calls](Interrupted-System-Calls.html#Interrupted-System-Calls)]
:::
