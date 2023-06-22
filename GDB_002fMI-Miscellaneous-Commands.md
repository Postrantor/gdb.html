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

Normally, thread groups that are being debugged are reported. With the '`--available` reports thread groups available on the target.

The output of this command may have either a '`threads`' result is described below.

To reduce the number of roundtrips it's possible to list thread groups together with their children, by passing the '`--recurse`' field.

In general, any combination of option and parameters is permitted, with the following caveats:

- When a single thread group is passed, the output will typically be the '`threads`' option will be ignored.
- When the '`--available`' is always an expensive operation and cache the results.

The '`groups`' result is a list of tuples, where each tuple may have the following fields:

`id`

:   Identifier of the thread group. This field is always present. The identifier is an opaque string; frontends should not try to convert it to an integer, even though it might look like one.

`type`

:   The type of the thread group. At present, only '`process`' is a valid type.

`pid`

:   The target-specific process identifier. This field is only present for thread groups of type '`process`' and only if the process exists.

`exit-code`

:   The exit code of this group's last exited thread, formatted in octal. This field is only present for thread groups of type '`process`' and only if the process is not running.

`num_children`

:   The number of children this thread group has. This field may be absent for an available thread group.

`threads`

:   This field has a list of tuples as value, each tuple describing a thread. It may be present if the '`--recurse`' option is specified, and it's actually possible to obtain the threads.

`cores`

:   This field is a list of integers, each identifying a core that one thread of the group is running on. This field may be absent if such information is not available.

`executable`

:   The name of the executable file that corresponds to this thread group. The field is only present for thread groups of type '`process`', and only if there is a corresponding executable file.

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

The types of information available depend on the target operating system.

#### [GDB]

The corresponding [GDB]'.

#### Example

When run on a [GNU]/Linux system, the output will look something like this:

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

#### The `-add-inferior` Command

#### Synopsis

::: smallexample

```bash
-add-inferior [ --no-connection ]
```

:::

Creates a new inferior (see [Inferiors Connections and Programs](Inferiors-Connections-and-Programs.html#Inferiors-Connections-and-Programs)). The created inferior is not associated with any executable. Such association may be established with the '`-file-exec-and-symbols`' command (see [GDB/MI File Commands](GDB_002fMI-File-Commands.html#GDB_002fMI-File-Commands)).

By default, the new inferior begins connected to the same target connection as the current inferior. For example, if the current inferior was connected to `gdbserver` with `target remote`, then the new inferior will be connected to the same `gdbserver` instance. The '`--no-connection`' option starts the new inferior with no connection yet. You can then for example use the `-target-select remote` command to connect to some other `gdbserver` instance, use `-exec-run` to spawn a local program, etc.

The command response always has a field, `inferior`, whose value is the identifier of the thread group corresponding to the new inferior.

An additional section field, `connection`, is optional. This field will only exist if the new inferior has a target connection. If this field exists, then its value will be a tuple containing the following fields:

'`number`'

:   The number of the connection used for the new inferior.

'`name`'

:   The name of the connection type used for the new inferior.

#### [GDB]

The corresponding [GDB]'](Inferiors-Connections-and-Programs.html#add_005finferior_005fcli)).

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

When an inferior is successfully removed a `=thread-group-removed` notification (see [GDB/MI Async Records](GDB_002fMI-Async-Records.html#GDB_002fMI-Async-Records)) is emitted, the `id` for the removed inferior.

#### [GDB]

The corresponding [GDB]'](Inferiors-Connections-and-Programs.html#remove_005finferiors_005fcli)).

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

#### Result

The result consists of two or three fields:

'`completion`'

:   This field contains the completed `command` has no known completions, this field is omitted.

'`matches`'

:   This field contains a (possibly empty) array of matches. It is always present.

'`max_completions_reached`'

:   This field contains `1` if number of known completions is above `max-completions` limit (see [Completion](Completion.html#Completion)), otherwise it contains `0`. It is always present.

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
