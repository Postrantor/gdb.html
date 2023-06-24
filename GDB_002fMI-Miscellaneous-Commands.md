---
tip: translate by openai@2023-06-23 22:01:11
...
---
description: GDB/MI Miscellaneous Commands (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: GDB/MI Miscellaneous Commands (Debugging with GDB)
lang: en
resource-type: document
title: GDB/MI Miscellaneous Commands (Debugging with GDB)
---
::: header
Previous: [GDB/MI Support Commands](GDB_002fMI-Support-Commands.html#GDB_002fMI-Support-Commands)]
:::

---

### 27.24 Miscellaneous [GDB/MI]

#### The `-gdb-exit` Command

#### Synopsis

::: smallexample

```bash
 -gdb-exit
```

:::

Exit [GDB] immediately.

#### [GDB]

Approximately corresponds to '`quit`'.

#### Example

::: smallexample

```bash
(gdb)
-gdb-exit
^exit
```

:::

#### The `-gdb-set` Command

#### Synopsis

::: smallexample

```bash
 -gdb-set
```

:::

Set an internal [GDB] variable.

#### [GDB]

The corresponding [GDB]'.

#### Example

::: smallexample

```bash
(gdb)
-gdb-set $foo=3
^done
(gdb)
```

:::

#### The `-gdb-show` Command

#### Synopsis

::: smallexample

```bash
 -gdb-show
```

:::

Show the current value of a [GDB] variable.

#### [GDB]

The corresponding [GDB]'.

#### Example

::: smallexample

```bash
(gdb)
-gdb-show annotate
^done,value="0"
(gdb)
```

:::

#### The `-gdb-version` Command

#### Synopsis

::: smallexample

```bash
 -gdb-version
```

:::

Show version information for [GDB]. Used mostly in testing.

#### [GDB]


The [GDB] by default shows this information when you start an interactive session.

> 默认情况下，当你启动交互会话时，[GDB]会显示这些信息。

#### Example

::: smallexample

```bash
(gdb)
-gdb-version
~GNU gdb 5.2.1
~Copyright 2000 Free Software Foundation, Inc.
~GDB is free software, covered by the GNU General Public License, and
~you are welcome to change it and/or distribute copies of it under
~ certain conditions.
~Type "show copying" to see the conditions.
~There is absolutely no warranty for GDB.  Type "show warranty" for
~ details.
~This GDB was configured as
 "--host=sparc-sun-solaris2.5.1 --target=ppc-eabi".
^done
(gdb)
```

:::

#### The `-list-thread-groups` Command

#### Synopsis

::: smallexample

```bash
-list-thread-groups [ --available ] [ --recurse 1 ] [ group ... ]
```

:::


Lists thread groups (see [Thread groups](Thread-groups.html#Thread-groups)). When a single thread group is passed as the argument, lists the children of that group. When several thread group are passed, lists information about those thread groups. Without any parameters, lists information about all top-level thread groups.

> 列出线程组（参见[线程组](Thread-groups.html#Thread-groups)）。当传递单个线程组作为参数时，列出该组的子组。当传递多个线程组时，列出有关这些线程组的信息。如果没有任何参数，列出有关所有顶级线程组的信息。


Normally, thread groups that are being debugged are reported. With the '`--available` reports thread groups available on the target.

> 通常，调试的线程组会被报告。使用'--available'报告可在目标上使用的线程组。


The output of this command may have either a '`threads`' result is described below.

> 此命令的输出可能具有“线程”结果，如下所述。


To reduce the number of roundtrips it's possible to list thread groups together with their children, by passing the '`--recurse`' field.

> 为了减少往返次数，可以通过传递'--recurse'字段将线程组及其子线程一起列出来。


In general, any combination of option and parameters is permitted, with the following caveats:

> 一般而言，允许使用任何选项和参数的组合，但需要注意以下几点：


- When a single thread group is passed, the output will typically be the '`threads`' option will be ignored.

> 当只传递一个线程组时，输出通常会忽略 'threads' 选项。
- When the '`--available`' is always an expensive operation and cache the results.


The '`groups`' result is a list of tuples, where each tuple may have the following fields:

> 'groups'结果是一个元组列表，每个元组可能包含以下字段：

`id`


:   Identifier of the thread group. This field is always present. The identifier is an opaque string; frontends should not try to convert it to an integer, even though it might look like one.

> 线程组的标识符。这个字段总是存在的。标识符是一个不透明的字符串；前端不应该尝试将其转换为整数，即使它看起来像一个整数。

`type`


:   The type of the thread group. At present, only '`process`' is a valid type.

> 线程组的类型。目前，只有'process'是有效的类型。

`pid`


:   The target-specific process identifier. This field is only present for thread groups of type '`process`' and only if the process exists.

> 目标特定的进程标识符。此字段仅存在于类型为“进程”的线程组中，并且仅在进程存在时才存在。

`exit-code`


:   The exit code of this group's last exited thread, formatted in octal. This field is only present for thread groups of type '`process`' and only if the process is not running.

> 這個組別上次退出的執行緒的退出碼，以八進位格式表示。此欄位僅適用於類型為'process'的執行緒組，且只有在該處理序未運行時才會出現。

`num_children`


:   The number of children this thread group has. This field may be absent for an available thread group.

> 这个线程组有多少个孩子？这个字段可能对可用的线程组缺失。

`threads`


:   This field has a list of tuples as value, each tuple describing a thread. It may be present if the '`--recurse`' option is specified, and it's actually possible to obtain the threads.

> 这个字段有一个元组列表作为值，每个元组描述一个线程。如果指定了'--recurse'选项，它可能存在，实际上可以获取线程。

`cores`


:   This field is a list of integers, each identifying a core that one thread of the group is running on. This field may be absent if such information is not available.

> 这个字段是一个整数列表，每个整数标识组中一个线程正在运行的核心。如果没有此类信息，此字段可能不存在。

`executable`


:   The name of the executable file that corresponds to this thread group. The field is only present for thread groups of type '`process`', and only if there is a corresponding executable file.

> 此线程组对应的可执行文件的名称。该字段仅适用于类型为'process'的线程组，并且仅在有相应的可执行文件时才存在。

#### Example

::: smallexample

```bash
(gdb)
-list-thread-groups
^done,groups=
-list-thread-groups 17
^done,threads=[{id="2",target-id="Thread 0xb7e14b90 (LWP 21257)",
   frame=,
{id="1",target-id="Thread 0xb7e156b0 (LWP 21254)",
   frame=],
           file="/tmp/a.c",fullname="/tmp/a.c",line="158",arch="i386:x86_64"},state="running"}]]
-list-thread-groups --available
^done,groups=
-list-thread-groups --available --recurse 1
 ^done,groups=[{id="17", types="process",pid="yyy",num_children="2",cores=[1,2],
                threads=[,
                         ,..]
-list-thread-groups --available --recurse 1 17 18
^done,groups=[{id="17", types="process",pid="yyy",num_children="2",cores=[1,2],
               threads=[,
                        ,...]
```

:::

#### The `-info-os` Command

#### Synopsis

::: smallexample

```bash
-info-os [ type ]
```

:::


If no argument is supplied, the command returns a table of available operating-system-specific information types. If one of these types is supplied as an argument `type`, then the command returns a table of data of that type.

> 如果没有提供参数，该命令会返回可用的操作系统特定信息类型的表格。如果其中一种类型被提供为参数'type'，那么该命令会返回该类型的数据表。

The types of information available depend on the target operating system.

#### [GDB]

The corresponding [GDB]'.

#### Example


When run on a [GNU]/Linux system, the output will look something like this:

> 当在GNU/Linux系统上运行时，输出看起来会像这样：

::: smallexample

```bash
(gdb)
-info-os
^done,OSDataTable={nr_rows="10",nr_cols="3",
hdr=[,
     ,
     ],
body=[item={col0="cpus",col1="Listing of all cpus/cores on the system",
            col2="CPUs"},
      item={col0="files",col1="Listing of all file descriptors",
            col2="File descriptors"},
      item={col0="modules",col1="Listing of all loaded kernel modules",
            col2="Kernel modules"},
      item={col0="msg",col1="Listing of all message queues",
            col2="Message queues"},
      item={col0="processes",col1="Listing of all processes",
            col2="Processes"},
      item={col0="procgroups",col1="Listing of all process groups",
            col2="Process groups"},
      item={col0="semaphores",col1="Listing of all semaphores",
            col2="Semaphores"},
      item={col0="shm",col1="Listing of all shared-memory regions",
            col2="Shared-memory regions"},
      item={col0="sockets",col1="Listing of all internet-domain sockets",
            col2="Sockets"},
      item={col0="threads",col1="Listing of all threads",
            col2="Threads"}]
(gdb)
-info-os processes
^done,OSDataTable={nr_rows="190",nr_cols="4",
hdr=[,
     ,
     ,
     ],
body=[item=,
      item=,
      item=,
      ...
      item=,
      item=
(gdb)
```

:::


(Note that the MI output here includes a `"Title"` column that does not appear in command-line `info os`; this column is useful for MI clients that want to enumerate the types of data, such as in a popup menu, but is needless clutter on the command line, and `info os` omits it.)

> （注意，这里的MI输出包括一个命令行`info os`中不存在的`"Title"`列；这一列对于希望枚举数据类型（如弹出菜单）的MI客户端很有用，但对命令行来说只是杂乱无章，因此`info os`省略了它。）

#### The `-add-inferior` Command

#### Synopsis

::: smallexample

```bash
-add-inferior [ --no-connection ]
```

:::


Creates a new inferior (see [Inferiors Connections and Programs](Inferiors-Connections-and-Programs.html#Inferiors-Connections-and-Programs)). The created inferior is not associated with any executable. Such association may be established with the '`-file-exec-and-symbols`' command (see [GDB/MI File Commands](GDB_002fMI-File-Commands.html#GDB_002fMI-File-Commands)).

> 创建一个新的次级（参见[次级连接和程序]（Inferiors-Connections-and-Programs.html#Inferiors-Connections-and-Programs））。创建的次级不与任何可执行文件相关联。可以使用 '-file-exec-and-symbols' 命令（参见[GDB/MI文件命令]（GDB_002fMI-File-Commands.html#GDB_002fMI-File-Commands））来建立该关联。


By default, the new inferior begins connected to the same target connection as the current inferior. For example, if the current inferior was connected to `gdbserver` with `target remote`, then the new inferior will be connected to the same `gdbserver` instance. The '`--no-connection`' option starts the new inferior with no connection yet. You can then for example use the `-target-select remote` command to connect to some other `gdbserver` instance, use `-exec-run` to spawn a local program, etc.

> 默认情况下，新的次要开始连接到与当前次要相同的目标连接。例如，如果当前次要已连接到`gdbserver`，使用`target remote`，那么新的次要将连接到相同的`gdbserver`实例。使用`--no-connection`选项可以启动新的次要，但尚未建立连接。然后，您可以使用`-target-select remote`命令连接到其他`gdbserver`实例，使用`-exec-run`来产生本地程序等。


The command response always has a field, `inferior`, whose value is the identifier of the thread group corresponding to the new inferior.

> 命令响应总是有一个字段“inferior”，其值是与新的次级对应的线程组的标识符。


An additional section field, `connection`, is optional. This field will only exist if the new inferior has a target connection. If this field exists, then its value will be a tuple containing the following fields:

> 另一个可选的部分字段`connection`。如果新的下级有目标连接，这个字段就会存在。如果这个字段存在，它的值将是一个包含以下字段的元组：

'`number`'

:   The number of the connection used for the new inferior.

'`name`'

:   The name of the connection type used for the new inferior.

#### [GDB]


The corresponding [GDB]'](Inferiors-Connections-and-Programs.html#add_005finferior_005fcli)).

> 相应的[GDB]

#### Example

::: smallexample

```bash
(gdb)
-add-inferior
^done,inferior="i3"
```

:::

#### The `-remove-inferior` Command

#### Synopsis

::: smallexample

```bash
-remove-inferior inferior-id
```

:::


Removes an inferior (see [Inferiors Connections and Programs](Inferiors-Connections-and-Programs.html#Inferiors-Connections-and-Programs)). Only inferiors that have exited can be removed. The `inferior-id`' command.

> 移除一个下级（参见[下级连接和程序]（Inferiors-Connections-and-Programs.html#Inferiors-Connections-and-Programs））。只有已退出的下级才能被移除。命令`inferior-id`。


When an inferior is successfully removed a `=thread-group-removed` notification (see [GDB/MI Async Records](GDB_002fMI-Async-Records.html#GDB_002fMI-Async-Records)) is emitted, the `id` for the removed inferior.

> 当一个次级被成功移除时，会发出`thread-group-removed`通知（参见[GDB/MI异步记录]），移除次级的`id`。

#### [GDB]


The corresponding [GDB]'](Inferiors-Connections-and-Programs.html#remove_005finferiors_005fcli)).

> 相应的[GDB]

#### Example

::: smallexample

```bash
(gdb)
-remove-inferior i3
=thread-group-removed,id="i3"
^done
```

:::

#### The `-interpreter-exec` Command

#### Synopsis

::: smallexample

```bash
-interpreter-exec interpreter command
```

:::

Execute the specified `command`.

#### [GDB]

The corresponding [GDB]'.

#### Example

::: smallexample

```bash
(gdb)
-interpreter-exec console "break main"
&"During symbol reading, couldn't parse type; debugger out of date?.\n"
&"During symbol reading, bad structure-type format.\n"
~"Breakpoint 1 at 0x8074fc6: file ../../src/gdb/main.c, line 743.\n"
^done
(gdb)
```

:::

#### The `-inferior-tty-set` Command

#### Synopsis

::: smallexample

```bash
-inferior-tty-set /dev/pts/1
```

:::

Set terminal for future runs of the program being debugged.

#### [GDB]

The corresponding [GDB]' /dev/pts/1.

#### Example

::: smallexample

```bash
(gdb)
-inferior-tty-set /dev/pts/1
^done
(gdb)
```

:::

#### The `-inferior-tty-show` Command

#### Synopsis

::: smallexample

```bash
-inferior-tty-show
```

:::

Show terminal for future runs of program being debugged.

#### [GDB]

The corresponding [GDB]'.

#### Example

::: smallexample

```bash
(gdb)
-inferior-tty-set /dev/pts/1
^done
(gdb)
-inferior-tty-show
^done,inferior_tty_terminal="/dev/pts/1"
(gdb)
```

:::

#### The `-enable-timings` Command

#### Synopsis

::: smallexample

```bash
-enable-timings [yes | no]
```

:::


Toggle the printing of the wallclock, user and system times for an MI command as a field in its output. This command is to help frontend developers optimize the performance of their code. No argument is equivalent to '`yes`'.

> 切换MI命令的输出中的墙上时钟、用户和系统时间的打印。此命令旨在帮助前端开发人员优化其代码的性能。没有参数等效于'yes'。

#### [GDB]

No equivalent.

#### Example

::: smallexample

```bash
(gdb)
-enable-timings
^done
(gdb)
-break-insert main
^done,bkpt={number="1",type="breakpoint",disp="keep",enabled="y",
addr="0x080484ed",func="main",file="myprog.c",
fullname="/home/nickrob/myprog.c",line="73",thread-groups=["i1"],
times="0"},
time=
(gdb)
-enable-timings no
^done
(gdb)
-exec-run
^running
(gdb)
*stopped,reason="breakpoint-hit",disp="keep",bkptno="1",thread-id="0",
frame=,
],file="myprog.c",
fullname="/home/nickrob/myprog.c",line="73",arch="i386:x86_64"}
(gdb)
```

:::

#### The `-complete` Command

#### Synopsis

::: smallexample

```bash
-complete command
```

:::

Show a list of completions for partially typed CLI `command`.


This command is intended for [GDB/MI] is used remotely via a SSH connection.

> 这个命令旨在为[GDB/MI]通过SSH连接远程使用。

#### Result

The result consists of two or three fields:

'`completion`'


:   This field contains the completed `command` has no known completions, this field is omitted.

> 这个字段包含已完成的命令，没有已知的完成，则会省略此字段。

'`matches`'


:   This field contains a (possibly empty) array of matches. It is always present.

> 这个字段包含一个（可能是空的）匹配数组。它总是存在的。

'`max_completions_reached`'


:   This field contains `1` if number of known completions is above `max-completions` limit (see [Completion](Completion.html#Completion)), otherwise it contains `0`. It is always present.

> 此字段包含1，如果已知完成数量超过最大完成数量限制（参见[完成](Completion.html#Completion))，否则它包含0。它总是存在的。

#### [GDB]

The corresponding [GDB]'.

#### Example

::: smallexample

```bash
(gdb)
-complete br
^done,completion="break",
      matches=["break","break-range"],
      max_completions_reached="0"
(gdb)
-complete "b ma"
^done,completion="b ma",
      matches=["b madvise","b main"],max_completions_reached="0"
(gdb)
-complete "b push_b"
^done,completion="b push_back(",
      matches=[
       "b A::push_back(void*)",
       "b std::string::push_back(char)",
       "b std::vector<int, std::allocator<int> >::push_back(int&&)"],
      max_completions_reached="0"
(gdb)
-complete "nonexist"
^done,matches=,max_completions_reached="0"
(gdb)
```

:::

---

::: header
Previous: [GDB/MI Support Commands](GDB_002fMI-Support-Commands.html#GDB_002fMI-Support-Commands)]
:::
