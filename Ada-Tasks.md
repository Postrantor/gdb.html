---
tip: translate by openai@2023-06-23 16:59:53
...
---
description: Ada Tasks (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Ada Tasks (Debugging with GDB)
lang: en
resource-type: document
title: Ada Tasks (Debugging with GDB)
---
::: header
Next: [Ada Tasks and Core Files](Ada-Tasks-and-Core-Files.html#Ada-Tasks-and-Core-Files)]
:::

---

#### 15.4.10.7 Extensions for Ada Tasks


Support for Ada tasks is analogous to that for threads (see [Threads](Threads.html#Threads)). [GDB] provides the following task-related commands:

> Ada任务的支持类似于线程的支持（参见[线程]（Threads.html＃Threads））。 [GDB]提供以下与任务相关的命令：

`info tasks`


This command shows a list of current Ada tasks, as in the following example:

> 这个命令显示当前Ada任务的列表，如下例所示：

::: smallexample

```bash
(gdb) info tasks
  ID       TID P-ID Pri State                 Name
   1   8088000   0   15 Child Activation Wait main_task
   2   80a4000   1   15 Accept Statement      b
   3   809a800   1   15 Child Activation Wait a
*  4   80ae800   3   15 Runnable              c
```

:::


In this listing, the asterisk before the last task indicates it to be the task currently being inspected.

> 在这个列表中，最后一项任务前面的星号表示它是当前正在检查的任务。

ID


:   Represents [GDB]'s internal task number.

> 表示GDB的内部任务号。

TID

:   The Ada task ID.

P-ID


:   The parent's task ID ([GDB]'s internal task number).

> 父母的任务ID（（GDB）的内部任务编号）。

Pri


:   The base priority of the task.

> 任务的基本优先级。

State


:   Current state of the task.

> 当前任务的状态

```
`Unactivated`

:   The task has been created but has not been activated. It cannot be executing.

`Runnable`

:   The task is not blocked for any reason known to Ada. (It may be waiting for a mutex, though.) It is conceptually \"executing\" in normal mode.

`Terminated`

:   The task is terminated, in the sense of ARM 9.3 (5). Any dependents that were waiting on terminate alternatives have been awakened and have terminated themselves.

`Child Activation Wait`

:   The task is waiting for created tasks to complete activation.

`Accept or Select Term`

:   The task is waiting on an accept or selective wait statement.

`Waiting on entry call`

:   The task is waiting on an entry call.

`Async Select Wait`

:   The task is waiting to start the abortable part of an asynchronous select statement.

`Delay Sleep`

:   The task is waiting on a select statement with only a delay alternative open.

`Child Termination Wait`

:   The task is sleeping having completed a master within itself, and is waiting for the tasks dependent on that master to become terminated or waiting on a terminate Phase.

`Wait Child in Term Alt`

:   The task is sleeping waiting for tasks on terminate alternatives to finish terminating.

`Asynchronous Hold`

:   The task has been held by `Ada.Asynchronous_Task_Control.Hold_Task`.

`Activating`

:   The task has been created and is being made runnable.

`Selective Wait`

:   The task is waiting in a selective wait statement.

`Accepting RV with taskno`

:   The task is accepting a rendez-vous with the task `taskno`.

`Waiting on RV with taskno`

:   The task is waiting for a rendez-vous with the task `taskno`.
```

Name


:   Name of the task in the program.

> 任务名称

`info task taskno`


This command shows detailed information on the specified task, as in the following example:

> 这个命令显示指定任务的详细信息，如下例所示：

::: smallexample

```bash
(gdb) info tasks
  ID       TID P-ID Pri State                  Name
   1   8077880    0  15 Child Activation Wait  main_task
*  2   807c468    1  15 Runnable               task_1
(gdb) info task 2
Ada Task: 0x807c468
Name: "task_1"
Thread: 0
LWP: 0x1fac
Parent: 1 ("main_task")
Base Priority: 15
State: Runnable
```

:::

`task`


This command prints the ID and name of the current task.

> 这个命令打印出当前任务的ID和名称。

::: smallexample

```bash
(gdb) info tasks
  ID       TID P-ID Pri State                  Name
   1   8077870    0  15 Child Activation Wait  main_task
*  2   807c458    1  15 Runnable               some_task
(gdb) task
[Current task is 2 "some_task"]
```

:::

`task taskno`


This command is like the `thread thread-id` command (see [Threads](Threads.html#Threads)). It switches the context of debugging from the current task to the given task.

> 这个命令类似于`thread thread-id`命令（参见[Threads](Threads.html#Threads)）。它将调试的上下文从当前任务切换到给定的任务。

::: smallexample

```bash
(gdb) info tasks
  ID       TID P-ID Pri State                  Name
   1   8077870    0  15 Child Activation Wait  main_task
*  2   807c458    1  15 Runnable               some_task
(gdb) task 1
[Switching to task 1 "main_task"]
#0  0x8067726 in pthread_cond_wait ()
(gdb) bt
#0  0x8067726 in pthread_cond_wait ()
#1  0x8056714 in system.os_interface.pthread_cond_wait ()
#2  0x805cb63 in system.task_primitives.operations.sleep ()
#3  0x806153e in system.tasking.stages.activate_tasks ()
#4  0x804aacc in un () at un.adb:5
```

:::

`task apply [task-id-list | all] [flag]… command`


The `task apply` command is the Ada tasking analogue of `thread apply` (see [Threads](Threads.html#Threads)). It allows you to apply the named `command` to one or more tasks. Specify the tasks that you want affected using a list of task IDs, or specify `all` to apply to all tasks.

> 命令`task apply`是Ada任务的类似物`thread apply`（参见[线程](Threads.html#Threads)）。它允许您将指定的`命令`应用于一个或多个任务。使用任务ID列表指定要受影响的任务，或指定`all`以将其应用于所有任务。


The `flag` must start with a `-` directly followed by one letter in `qcs`. If several flags are provided, they must be given individually, such as `-c -q`.

> 标志必须以一个"-"开头，直接跟着qcs中的一个字母。如果提供了多个标志，它们必须分开，比如"-c -q"。


By default, [GDB] will abort `task apply`. The following flags can be used to fine-tune this behavior:

> 默认情况下，GDB会中止“任务应用”。以下标志可用于微调此行为：

`-c`


:   The flag `-c`, which stands for '`continue` to be displayed, and the execution of `task apply` then continues.

> 标志'-c'代表'继续'，然后继续执行'task apply'。

`-s`


:   The flag `-s`, which stands for '`silent` to be silently ignored. That is, the execution continues, but the task information and errors are not printed.

> 标志'-s'代表“静默”，将被静默忽略。也就是说，执行会继续，但任务信息和错误不会被打印出来。

`-q`


:   The flag `-q` ('`quiet`') disables printing the task information.

> `-q` 标志（"quiet"）可禁用打印任务信息。


Flags `-c` and `-s` cannot be used together.

> 标志`-c`和`-s`不能同时使用。

`break locspec task taskno`

`break locspec task taskno if …`


These commands are like the `break … thread …` command (see [Thread Stops](Thread-Stops.html#Thread-Stops)). See [Location Specifications](Location-Specifications.html#Location-Specifications), for the various forms of `locspec`.

> 这些命令类似于`break ... thread ...`命令（参见[线程停止](Thread-Stops.html#Thread-Stops)）。参见[位置规范](Location-Specifications.html#Location-Specifications)，了解各种形式的`locspec`。


Use the qualifier '`task taskno`' display.

> 使用限定词“任务号”显示。


If you do not specify '`task taskno`' when you set a breakpoint, the breakpoint applies to *all* tasks of your program.

> 如果你在设置断点时没有指定'task taskno'，那么断点将适用于程序的所有任务。


You can use the `task` qualifier on conditional breakpoints as well; in this case, place '`task taskno`' before the breakpoint condition (before the `if`).

> 您也可以在条件断点上使用`task`限定符；在这种情况下，在断点条件（`if`之前）之前放置'`task taskno`'。

For example,

::: smallexample

```bash
(gdb) info tasks
  ID       TID P-ID Pri State                 Name
   1 140022020   0   15 Child Activation Wait main_task
   2 140045060   1   15 Accept/Select Wait    t2
   3 140044840   1   15 Runnable              t1
*  4 140056040   1   15 Runnable              t3
(gdb) b 15 task 2
Breakpoint 5 at 0x120044cb0: file test_task_debug.adb, line 15.
(gdb) cont
Continuing.
task # 1 running
task # 2 running

Breakpoint 5, test_task_debug () at test_task_debug.adb:15
15               flush;
(gdb) info tasks
  ID       TID P-ID Pri State                 Name
   1 140022020   0   15 Child Activation Wait main_task
*  2 140045060   1   15 Runnable              t2
   3 140044840   1   15 Runnable              t1
   4 140056040   1   15 Delay Sleep           t3
```

:::

---

::: header
Next: [Ada Tasks and Core Files](Ada-Tasks-and-Core-Files.html#Ada-Tasks-and-Core-Files)]
:::
