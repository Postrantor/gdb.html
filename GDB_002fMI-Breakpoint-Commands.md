---
description: GDB/MI Breakpoint Commands (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: GDB/MI Breakpoint Commands (Debugging with GDB)
lang: en
resource-type: document
title: GDB/MI Breakpoint Commands (Debugging with GDB)
---
::: header
Next: [GDB/MI Catchpoint Commands](GDB_002fMI-Catchpoint-Commands.html#GDB_002fMI-Catchpoint-Commands)]
:::

---

### 27.8 [GDB/MI]

This section documents [GDB/MI] commands for manipulating breakpoints.

#### The `-break-after` Command

#### Synopsis

::: smallexample

```bash
 -break-after number count
```

:::

The breakpoint number `number`' command below.

#### [GDB]

The corresponding [GDB]'.

#### Example

::: smallexample

```bash
(gdb)
-break-insert main
^done,bkpt={number="1",type="breakpoint",disp="keep",
enabled="y",addr="0x000100d0",func="main",file="hello.c",
fullname="/home/foo/hello.c",line="5",thread-groups=["i1"],
times="0"}
(gdb)
-break-after 1 3
~
^done
(gdb)
-break-list
^done,BreakpointTable={nr_rows="1",nr_cols="6",
hdr=[,
,
,
,
,
],
body=[bkpt={number="1",type="breakpoint",disp="keep",enabled="y",
addr="0x000100d0",func="main",file="hello.c",fullname="/home/foo/hello.c",
line="5",thread-groups=["i1"],times="0",ignore="3"}]}
(gdb)
```

:::

#### The `-break-commands` Command

#### Synopsis

::: smallexample

```bash
 -break-commands number [ command1 ... commandN ]
```

:::

Specifies the CLI commands that should be executed when breakpoint `number` are the commands. If no command is specified, any previously-set commands are cleared. See [Break Commands](Break-Commands.html#Break-Commands). Typical use of this functionality is tracing a program, that is, printing of values of some variables whenever breakpoint is hit and then continuing.

#### [GDB]

The corresponding [GDB]'.

#### Example

::: smallexample

```bash
(gdb)
-break-insert main
^done,bkpt={number="1",type="breakpoint",disp="keep",
enabled="y",addr="0x000100d0",func="main",file="hello.c",
fullname="/home/foo/hello.c",line="5",thread-groups=["i1"],
times="0"}
(gdb)
-break-commands 1 "print v" "continue"
^done
(gdb)
```

:::

#### The `-break-condition` Command

#### Synopsis

::: smallexample

```bash
 -break-condition [ --force ] number [ expr ]
```

:::

Breakpoint `number` becomes unconditional.

#### [GDB]

The corresponding [GDB]'.

#### Example

::: smallexample

```bash
(gdb)
-break-condition 1 1
^done
(gdb)
-break-list
^done,BreakpointTable={nr_rows="1",nr_cols="6",
hdr=[,
,
,
,
,
],
body=[bkpt={number="1",type="breakpoint",disp="keep",enabled="y",
addr="0x000100d0",func="main",file="hello.c",fullname="/home/foo/hello.c",
line="5",cond="1",thread-groups=["i1"],times="0",ignore="3"}]}
(gdb)
```

:::

#### The `-break-delete` Command

#### Synopsis

::: smallexample

```bash
 -break-delete ( breakpoint )+
```

:::

Delete the breakpoint(s) whose number(s) are specified in the argument list. This is obviously reflected in the breakpoint list.

#### [GDB]

The corresponding [GDB]'.

#### Example

::: smallexample

```bash
(gdb)
-break-delete 1
^done
(gdb)
-break-list
^done,BreakpointTable={nr_rows="0",nr_cols="6",
hdr=[,
,
,
,
,
],
body=}
(gdb)
```

:::

#### The `-break-disable` Command

#### Synopsis

::: smallexample

```bash
 -break-disable ( breakpoint )+
```

:::

Disable the named `breakpoint`(s).

#### [GDB]

The corresponding [GDB]'.

#### Example

::: smallexample

```bash
(gdb)
-break-disable 2
^done
(gdb)
-break-list
^done,BreakpointTable={nr_rows="1",nr_cols="6",
hdr=[,
,
,
,
,
],
body=[bkpt={number="2",type="breakpoint",disp="keep",enabled="n",
addr="0x000100d0",func="main",file="hello.c",fullname="/home/foo/hello.c",
line="5",thread-groups=["i1"],times="0"}]}
(gdb)
```

:::

#### The `-break-enable` Command

#### Synopsis

::: smallexample

```bash
 -break-enable ( breakpoint )+
```

:::

Enable (previously disabled) `breakpoint`(s).

#### [GDB]

The corresponding [GDB]'.

#### Example

::: smallexample

```bash
(gdb)
-break-enable 2
^done
(gdb)
-break-list
^done,BreakpointTable={nr_rows="1",nr_cols="6",
hdr=[,
,
,
,
,
],
body=[bkpt={number="2",type="breakpoint",disp="keep",enabled="y",
addr="0x000100d0",func="main",file="hello.c",fullname="/home/foo/hello.c",
line="5",thread-groups=["i1"],times="0"}]}
(gdb)
```

:::

#### The `-break-info` Command

#### Synopsis

::: smallexample

```bash
 -break-info breakpoint
```

:::

Get information about a single breakpoint.

The result is a table of breakpoints. See [GDB/MI Breakpoint Information](GDB_002fMI-Breakpoint-Information.html#GDB_002fMI-Breakpoint-Information), for details on the format of each breakpoint in the table.

#### [GDB]

The corresponding [GDB]'.

#### Example

N.A.

#### The `-break-insert` Command

#### Synopsis

::: smallexample

```bash
 -break-insert [ -t ] [ -h ] [ -f ] [ -d ] [ -a ] [ --qualified ]
    [ -c condition ] [ --force-condition ] [ -i ignore-count ]
    [ -p thread-id ] [ locspec ]
```

:::

If specified, `locspec`, can be one of:

`linespec location`

:   A linespec location. See [Linespec Locations](Linespec-Locations.html#Linespec-Locations).

`explicit location`

:   An explicit location. [GDB/MI] explicit locations are analogous to the CLI's explicit locations using the option names listed below. See [Explicit Locations](Explicit-Locations.html#Explicit-Locations).

```
'`--source filename`'

:   The source file name of the location. This option requires the use of either '`--function`'.

'`--function function`'

:   The name of a function or method.

'`--label label`'

:   The name of a label.

'`--line lineoffset`'

:   An absolute or relative line offset from the start of the location.
```

`address location`

:   An address location, \*`address`. See [Address Locations](Address-Locations.html#Address-Locations).

The possible optional parameters of this command are:

'`-t`'

:   Insert a temporary breakpoint.

'`-h`'

:   Insert a hardware breakpoint.

'`-f`'

:   If `locspec` cannot be parsed.

'`-d`'

:   Create a disabled breakpoint.

'`-a`'

:   Create a tracepoint. See [Tracepoints](Tracepoints.html#Tracepoints). When this parameter is used together with '`-h`', a fast tracepoint is created.

'`-c condition`'

:   Make the breakpoint conditional on `condition`.

'`--force-condition`'

:   Forcibly define the breakpoint even if the condition is invalid at all of the breakpoint locations.

'`-i ignore-count`'

:   Initialize the `ignore-count`.

'`-p thread-id`'

:   Restrict the breakpoint to the thread with the specified global `thread-id` will automatically be deleted when the corresponding thread exits.

'`--qualified`'

:   This option makes [GDB] interpret a function name specified as a complete fully-qualified name.

#### Result

See [GDB/MI Breakpoint Information](GDB_002fMI-Breakpoint-Information.html#GDB_002fMI-Breakpoint-Information), for details on the format of the resulting breakpoint.

Note: this format is open to change.

#### [GDB]

The corresponding [GDB]'.

#### Example

::: smallexample

```bash
(gdb)
-break-insert main
^done,bkpt={number="1",addr="0x0001072c",file="recursive2.c",
fullname="/home/foo/recursive2.c,line="4",thread-groups=["i1"],
times="0"}
(gdb)
-break-insert -t foo
^done,bkpt={number="2",addr="0x00010774",file="recursive2.c",
fullname="/home/foo/recursive2.c,line="11",thread-groups=["i1"],
times="0"}
(gdb)
-break-list
^done,BreakpointTable={nr_rows="2",nr_cols="6",
hdr=[,
,
,
,
,
],
body=[bkpt={number="1",type="breakpoint",disp="keep",enabled="y",
addr="0x0001072c", func="main",file="recursive2.c",
fullname="/home/foo/recursive2.c,"line="4",thread-groups=["i1"],
times="0"},
bkpt={number="2",type="breakpoint",disp="del",enabled="y",
addr="0x00010774",func="foo",file="recursive2.c",
fullname="/home/foo/recursive2.c",line="11",thread-groups=["i1"],
times="0"}]}
(gdb)
```

:::

#### The `-dprintf-insert` Command

#### Synopsis

::: smallexample

```bash
 -dprintf-insert [ -t ] [ -f ] [ -d ] [ --qualified ]
    [ -c condition ] [--force-condition] [ -i ignore-count ]
    [ -p thread-id ] [ locspec ] format
    [ argument… ]
```

:::

Insert a new dynamic print breakpoint at the given location. See [Dynamic Printf](Dynamic-Printf.html#Dynamic-Printf). `format` is the format to use, and any remaining arguments are passed as expressions to substitute.

If supplied, `locspec` and `--qualified` may be specified the same way as for the `-break-insert` command. See [-break-insert](#g_t_002dbreak_002dinsert).

The possible optional parameters of this command are:

'`-t`'

:   Insert a temporary breakpoint.

'`-f`'

:   If `locspec` cannot be parsed.

'`-d`'

:   Create a disabled breakpoint.

'`-c condition`'

:   Make the breakpoint conditional on `condition`.

'`--force-condition`'

:   Forcibly define the breakpoint even if the condition is invalid at all of the breakpoint locations.

'`-i ignore-count`'

:   Set the ignore count of the breakpoint (see [ignore count](Conditions.html#Conditions)) to `ignore-count`.

'`-p thread-id`'

:   Restrict the breakpoint to the thread with the specified global `thread-id`.

#### Result

See [GDB/MI Breakpoint Information](GDB_002fMI-Breakpoint-Information.html#GDB_002fMI-Breakpoint-Information), for details on the format of the resulting breakpoint.

#### [GDB]

The corresponding [GDB]'.

#### Example

::: smallexample

```bash
(gdb)
4-dprintf-insert foo "At foo entry\n"
4^done,bkpt={number="1",type="dprintf",disp="keep",enabled="y",
addr="0x000000000040061b",func="foo",file="mi-dprintf.c",
fullname="mi-dprintf.c",line="25",thread-groups=["i1"],
times="0",script=["printf \"At foo entry\\n\"","continue"],
original-location="foo"}
(gdb)
5-dprintf-insert 26 "arg=%d, g=%d\n" arg g
5^done,bkpt={number="2",type="dprintf",disp="keep",enabled="y",
addr="0x000000000040062a",func="foo",file="mi-dprintf.c",
fullname="mi-dprintf.c",line="26",thread-groups=["i1"],
times="0",script=["printf \"arg=%d, g=%d\\n\", arg, g","continue"],
original-location="mi-dprintf.c:26"}
(gdb)
```

:::

#### The `-break-list` Command

#### Synopsis

::: smallexample

```bash
 -break-list
```

:::

Displays the list of inserted breakpoints, showing the following fields:

'`Number`'

:   number of the breakpoint

'`Type`'

:   type of the breakpoint: '`breakpoint`'

'`Disposition`'

:   should the breakpoint be deleted or disabled when it is hit: '`keep`'

'`Enabled`'

:   is the breakpoint enabled or no: '`y`'

'`Address`'

:   memory location at which the breakpoint is set

'`What`'

:   logical location of the breakpoint, expressed by function name, file name, line number

'`Thread-groups`'

:   list of thread groups to which this breakpoint applies

'`Times`'

:   number of times the breakpoint has been hit

If there are no breakpoints or watchpoints, the `BreakpointTable` `body` field is an empty list.

#### [GDB]

The corresponding [GDB]'.

#### Example

::: smallexample

```bash
(gdb)
-break-list
^done,BreakpointTable={nr_rows="2",nr_cols="6",
hdr=[,
,
,
,
,
],
body=[bkpt={number="1",type="breakpoint",disp="keep",enabled="y",
addr="0x000100d0",func="main",file="hello.c",line="5",thread-groups=["i1"],
times="0"},
bkpt={number="2",type="breakpoint",disp="keep",enabled="y",
addr="0x00010114",func="foo",file="hello.c",fullname="/home/foo/hello.c",
line="13",thread-groups=["i1"],times="0"}]}
(gdb)
```

:::

Here's an example of the result when there are no breakpoints:

::: smallexample

```bash
(gdb)
-break-list
^done,BreakpointTable={nr_rows="0",nr_cols="6",
hdr=[,
,
,
,
,
],
body=}
(gdb)
```

:::

#### The `-break-passcount` Command

#### Synopsis

::: smallexample

```bash
 -break-passcount tracepoint-number passcount
```

:::

Set the passcount for tracepoint `tracepoint-number`'.

#### The `-break-watch` Command

#### Synopsis

::: smallexample

```bash
 -break-watch [ -a | -r ]
```

:::

Create a watchpoint. With the '`-a`' option, the watchpoint created is a *read* watchpoint, i.e., it will trigger only when the memory location is accessed for reading. Without either of the options, the watchpoint created is a regular watchpoint, i.e., it will trigger when the memory location is accessed for writing. See [Setting Watchpoints](Set-Watchpoints.html#Set-Watchpoints).

Note that '`-break-list`' will report a single list of watchpoints and breakpoints inserted.

#### [GDB]

The corresponding [GDB]'.

#### Example

Setting a watchpoint on a variable in the `main` function:

::: smallexample

```bash
(gdb)
-break-watch x
^done,wpt=
(gdb)
-exec-continue
^running
(gdb)
*stopped,reason="watchpoint-trigger",wpt=,
value=,
frame={func="main",args=,file="recursive2.c",
fullname="/home/foo/bar/recursive2.c",line="5",arch="i386:x86_64"}
(gdb)
```

:::

Setting a watchpoint on a variable local to a function. [GDB] will stop the program execution twice: first for the variable changing value, then for the watchpoint going out of scope.

::: smallexample

```bash
(gdb)
-break-watch C
^done,wpt=
(gdb)
-exec-continue
^running
(gdb)
*stopped,reason="watchpoint-trigger",
wpt=,
frame={func="callee4",args=,
file="../../../devo/gdb/testsuite/gdb.mi/basics.c",
fullname="/home/foo/bar/devo/gdb/testsuite/gdb.mi/basics.c",line="13",
arch="i386:x86_64"}
(gdb)
-exec-continue
^running
(gdb)
*stopped,reason="watchpoint-scope",wpnum="5",
frame={func="callee3",args=[{name="strarg",
value="0x11940 \"A string argument.\""}],
file="../../../devo/gdb/testsuite/gdb.mi/basics.c",
fullname="/home/foo/bar/devo/gdb/testsuite/gdb.mi/basics.c",line="18",
arch="i386:x86_64"}
(gdb)
```

:::

Listing breakpoints and watchpoints, at different points in the program execution. Note that once the watchpoint goes out of scope, it is deleted.

::: smallexample

```bash
(gdb)
-break-watch C
^done,wpt=
(gdb)
-break-list
^done,BreakpointTable={nr_rows="2",nr_cols="6",
hdr=[,
,
,
,
,
],
body=[bkpt={number="1",type="breakpoint",disp="keep",enabled="y",
addr="0x00010734",func="callee4",
file="../../../devo/gdb/testsuite/gdb.mi/basics.c",
fullname="/home/foo/devo/gdb/testsuite/gdb.mi/basics.c"line="8",thread-groups=["i1"],
times="1"},
bkpt={number="2",type="watchpoint",disp="keep",
enabled="y",addr="",what="C",thread-groups=["i1"],times="0"}]}
(gdb)
-exec-continue
^running
(gdb)
*stopped,reason="watchpoint-trigger",wpt=,
value=,
frame={func="callee4",args=,
file="../../../devo/gdb/testsuite/gdb.mi/basics.c",
fullname="/home/foo/bar/devo/gdb/testsuite/gdb.mi/basics.c",line="13",
arch="i386:x86_64"}
(gdb)
-break-list
^done,BreakpointTable={nr_rows="2",nr_cols="6",
hdr=[,
,
,
,
,
],
body=[bkpt={number="1",type="breakpoint",disp="keep",enabled="y",
addr="0x00010734",func="callee4",
file="../../../devo/gdb/testsuite/gdb.mi/basics.c",
fullname="/home/foo/devo/gdb/testsuite/gdb.mi/basics.c",line="8",thread-groups=["i1"],
times="1"},
bkpt={number="2",type="watchpoint",disp="keep",
enabled="y",addr="",what="C",thread-groups=["i1"],times="-5"}]}
(gdb)
-exec-continue
^running
^done,reason="watchpoint-scope",wpnum="2",
frame={func="callee3",args=[{name="strarg",
value="0x11940 \"A string argument.\""}],
file="../../../devo/gdb/testsuite/gdb.mi/basics.c",
fullname="/home/foo/bar/devo/gdb/testsuite/gdb.mi/basics.c",line="18",
arch="i386:x86_64"}
(gdb)
-break-list
^done,BreakpointTable={nr_rows="1",nr_cols="6",
hdr=[,
,
,
,
,
],
body=[bkpt={number="1",type="breakpoint",disp="keep",enabled="y",
addr="0x00010734",func="callee4",
file="../../../devo/gdb/testsuite/gdb.mi/basics.c",
fullname="/home/foo/devo/gdb/testsuite/gdb.mi/basics.c",line="8",
thread-groups=["i1"],times="1"}]}
(gdb)
```

:::

---

::: header
Next: [GDB/MI Catchpoint Commands](GDB_002fMI-Catchpoint-Commands.html#GDB_002fMI-Catchpoint-Commands)]
:::
