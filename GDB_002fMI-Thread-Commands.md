---
tip: translate by openai@2023-06-23 22:18:42
...
---
description: GDB/MI Thread Commands (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: GDB/MI Thread Commands (Debugging with GDB)
lang: en
resource-type: document
title: GDB/MI Thread Commands (Debugging with GDB)
---
::: header
Next: [GDB/MI Ada Tasking Commands](GDB_002fMI-Ada-Tasking-Commands.html#GDB_002fMI-Ada-Tasking-Commands)]
:::

---

### 27.11 [GDB/MI]

#### The `-thread-info` Command

#### Synopsis

::: smallexample

```bash
 -thread-info [ thread-id ]
```

:::


Reports information about either a specific thread, if the `thread-id` is the thread's global thread ID. When printing information about all threads, also reports the global ID of the current thread.

> 报告关于特定线程的信息，如果`thread-id`是线程的全局线程ID。当打印关于所有线程的信息时，还报告当前线程的全局ID。

#### [GDB]


The '`info thread`' command prints the same information about all threads.

> 命令"info thread"会打印出所有线程的相同信息。

#### Result

The result contains the following attributes:

'`threads`'


:   A list of threads. The format of the elements of the list is described in [GDB/MI Thread Information](GDB_002fMI-Thread-Information.html#GDB_002fMI-Thread-Information).

> 一个线程列表。列表元素的格式可以在[GDB/MI线程信息](GDB_002fMI-Thread-Information.html#GDB_002fMI-Thread-Information)中找到。

'`current-thread-id`'


:   The global id of the currently selected thread. This field is omitted if there is no selected thread (for example, when the selected inferior is not running, and therefore has no threads) or if a `thread-id` argument was passed to the command.

> 当前选定的线程的全局ID。如果没有选定的线程（例如，当所选择的下级未运行，因此没有线程）或者向命令传递了`thread-id`参数，则会省略此字段。

#### Example

::: smallexample

```bash
-thread-info
^done,threads=[
{id="2",target-id="Thread 0xb7e14b90 (LWP 21257)",
   frame={level="0",addr="0xffffe410",func="__kernel_vsyscall",
           args=},state="running"},
{id="1",target-id="Thread 0xb7e156b0 (LWP 21254)",
   frame={level="0",addr="0x0804891f",func="foo",
           args=,
           file="/tmp/a.c",fullname="/tmp/a.c",line="158",arch="i386:x86_64"},
           state="running"}],
current-thread-id="1"
(gdb)
```

:::

#### The `-thread-list-ids` Command

#### Synopsis

::: smallexample

```bash
 -thread-list-ids
```

:::


Produces a list of the currently known global [GDB] thread ids. At the end of the list it also prints the total number of such threads.

> 产生当前已知的全局[GDB]线程ID列表。在列表末尾也会打印出这些线程的总数。


This command is retained for historical reasons, the `-thread-info` command should be used instead.

> 这个命令出于历史原因而被保留，应该使用`-thread-info`命令代替。

#### [GDB]

Part of '`info threads`' supplies the same information.

#### Example

::: smallexample

```bash
(gdb)
-thread-list-ids
^done,thread-ids=,
current-thread-id="1",number-of-threads="3"
(gdb)
```

:::

#### The `-thread-select` Command

#### Synopsis

::: smallexample

```bash
 -thread-select thread-id
```

:::


Make thread with global thread number `thread-id` the current thread. It prints the number of the new current thread, and the topmost frame for that thread.

> 使用全局线程号`thread-id`创建线程，它将打印新当前线程的编号以及该线程的顶层框架。


This command is deprecated in favor of explicitly using the '`--thread`' option to each command.

> 这个命令已经被废弃，建议明确地使用'--thread'选项来调用每个命令。

#### [GDB]

The corresponding [GDB]'.

#### Example

::: smallexample

```bash
(gdb)
-exec-next
^running
(gdb)
*stopped,reason="end-stepping-range",thread-id="2",line="187",
file="../../../devo/gdb/testsuite/gdb.threads/linux-dp.c"
(gdb)
-thread-list-ids
^done,
thread-ids=,
number-of-threads="3"
(gdb)
-thread-select 3
^done,new-thread-id="3",
frame={level="0",func="vprintf",
args=[,

(gdb)
```

:::

---

::: header
Next: [GDB/MI Ada Tasking Commands](GDB_002fMI-Ada-Tasking-Commands.html#GDB_002fMI-Ada-Tasking-Commands)]
:::
