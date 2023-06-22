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

`info tasks`

This command shows a list of current Ada tasks, as in the following example:

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

ID

:   Represents [GDB]'s internal task number.

TID

:   The Ada task ID.

P-ID

:   The parent's task ID ([GDB]'s internal task number).

Pri

:   The base priority of the task.

State

:   Current state of the task.

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

`info task taskno`

This command shows detailed information on the specified task, as in the following example:

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

The `flag` must start with a `-` directly followed by one letter in `qcs`. If several flags are provided, they must be given individually, such as `-c -q`.

By default, [GDB] will abort `task apply`. The following flags can be used to fine-tune this behavior:

`-c`

:   The flag `-c`, which stands for '`continue` to be displayed, and the execution of `task apply` then continues.

`-s`

:   The flag `-s`, which stands for '`silent` to be silently ignored. That is, the execution continues, but the task information and errors are not printed.

`-q`

:   The flag `-q` ('`quiet`') disables printing the task information.

Flags `-c` and `-s` cannot be used together.

`break locspec task taskno`

`break locspec task taskno if …`

These commands are like the `break … thread …` command (see [Thread Stops](Thread-Stops.html#Thread-Stops)). See [Location Specifications](Location-Specifications.html#Location-Specifications), for the various forms of `locspec`.

Use the qualifier '`task taskno`' display.

If you do not specify '`task taskno`' when you set a breakpoint, the breakpoint applies to *all* tasks of your program.

You can use the `task` qualifier on conditional breakpoints as well; in this case, place '`task taskno`' before the breakpoint condition (before the `if`).

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
