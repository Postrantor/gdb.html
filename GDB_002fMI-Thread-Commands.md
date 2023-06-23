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

#### [GDB]

The '`info thread`' command prints the same information about all threads.

#### Result

The result contains the following attributes:

'`threads`'

:   A list of threads. The format of the elements of the list is described in [GDB/MI Thread Information](GDB_002fMI-Thread-Information.html#GDB_002fMI-Thread-Information).

'`current-thread-id`'

:   The global id of the currently selected thread. This field is omitted if there is no selected thread (for example, when the selected inferior is not running, and therefore has no threads) or if a `thread-id` argument was passed to the command.

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

This command is retained for historical reasons, the `-thread-info` command should be used instead.

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

This command is deprecated in favor of explicitly using the '`--thread`' option to each command.

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
