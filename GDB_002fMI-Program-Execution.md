---
description: GDB/MI Program Execution (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: GDB/MI Program Execution (Debugging with GDB)
lang: en
resource-type: document
title: GDB/MI Program Execution (Debugging with GDB)
---
::: header
Next: [GDB/MI Stack Manipulation](GDB_002fMI-Stack-Manipulation.html#GDB_002fMI-Stack-Manipulation)]
:::

---

### 27.13 [GDB/MI]

These are the asynchronous commands which generate the out-of-band record '`*stopped` only really executes asynchronously with remote targets and this interaction is mimicked in other cases.

#### The `-exec-continue` Command

#### Synopsis

::: smallexample

```bash
 -exec-continue [--reverse] [--all|--thread-group N]
```

:::

Resumes the execution of the inferior program, which will continue to execute until it reaches a debugger stop event. If the '`--reverse`' option is specified, execution resumes in reverse until it reaches a stop event. Stop events may include

- breakpoints or watchpoints
- signals or exceptions
- the end of the process (or its beginning under '`--reverse`')
- the end or beginning of a replay log if one is being used.

In all-stop mode (see [All-Stop Mode](All_002dStop-Mode.html#All_002dStop-Mode)), may resume only one thread, or all threads, depending on the value of the '`scheduler-locking`' options is specified, then all threads in that thread group are resumed.

#### [GDB]

The corresponding [GDB]'.

#### Example

::: smallexample

```bash
-exec-continue
^running
(gdb)
@Hello world
*stopped,reason="breakpoint-hit",disp="keep",bkptno="2",frame={
func="foo",args=,file="hello.c",fullname="/home/foo/bar/hello.c",
line="13",arch="i386:x86_64"}
(gdb)
```

:::

For a '`breakpoint-hit`'.

::: smallexample

```bash
-exec-continue
^running
(gdb)
@Hello world
*stopped,reason="breakpoint-hit",disp="keep",bkptno="2",locno="3",frame={
func="foo",args=,file="hello.c",fullname="/home/foo/bar/hello.c",
line="13",arch="i386:x86_64"}
(gdb)
```

:::

#### The `-exec-finish` Command

#### Synopsis

::: smallexample

```bash
 -exec-finish [--reverse]
```

:::

Resumes the execution of the inferior program until the current function is exited. Displays the results returned by the function. If the '`--reverse`' option is specified, resumes the reverse execution of the inferior program until the point where current function was called.

#### [GDB]

The corresponding [GDB]'.

#### Example

Function returning `void`.

::: smallexample

```bash
-exec-finish
^running
(gdb)
@hello from foo
*stopped,reason="function-finished",frame={func="main",args=,
file="hello.c",fullname="/home/foo/bar/hello.c",line="7",arch="i386:x86_64"}
(gdb)
```

:::

Function returning other than `void`. The name of the internal [GDB] variable storing the result is printed, together with the value itself.

::: smallexample

```bash
-exec-finish
^running
(gdb)
*stopped,reason="function-finished",frame={addr="0x000107b0",func="foo",
args=[,
file="recursive2.c",fullname="/home/foo/bar/recursive2.c",line="14",
arch="i386:x86_64"},
gdb-result-var="$1",return-value="0"
(gdb)
```

:::

#### The `-exec-interrupt` Command

#### Synopsis

::: smallexample

```bash
 -exec-interrupt [--all|--thread-group N]
```

:::

Interrupts the background execution of the target. Note how the token associated with the stop message is the one for the execution command that has been interrupted. The token for the interrupt itself only appears in the '`^done`' output. If the user is trying to interrupt a non-running program, an error message will be printed.

Note that when asynchronous execution is enabled, this command is asynchronous just like other execution commands. That is, first the '`^done`' notification.

In non-stop mode, only the context thread is interrupted by default. All threads (in all inferiors) will be interrupted if the '`--all`' option is specified, all threads in that group will be interrupted.

#### [GDB]

The corresponding [GDB]'.

#### Example

::: smallexample

```bash
(gdb)
111-exec-continue
111^running

(gdb)
222-exec-interrupt
222^done
(gdb)
111*stopped,signal-name="SIGINT",signal-meaning="Interrupt",
frame={addr="0x00010140",func="foo",args=,file="try.c",
fullname="/home/foo/bar/try.c",line="13",arch="i386:x86_64"}
(gdb)

(gdb)
-exec-interrupt
^error,msg="mi_cmd_exec_interrupt: Inferior not executing."
(gdb)
```

:::

#### The `-exec-jump` Command

#### Synopsis

::: smallexample

```bash
 -exec-jump locspec
```

:::

Resumes execution of the inferior program at the address to which `locspec`.

#### [GDB]

The corresponding [GDB]'.

#### Example

::: smallexample

```bash
-exec-jump foo.c:10
*running,thread-id="all"
^running
```

:::

#### The `-exec-next` Command

#### Synopsis

::: smallexample

```bash
 -exec-next [--reverse]
```

:::

Resumes execution of the inferior program, stopping when the beginning of the next source line is reached.

If the '`--reverse`' option is specified, resumes reverse execution of the inferior program, stopping at the beginning of the previous source line. If you issue this command on the first line of a function, it will take you back to the caller of that function, to the source line where the function was called.

#### [GDB]

The corresponding [GDB]'.

#### Example

::: smallexample

```bash
-exec-next
^running
(gdb)
*stopped,reason="end-stepping-range",line="8",file="hello.c"
(gdb)
```

:::

#### The `-exec-next-instruction` Command

#### Synopsis

::: smallexample

```bash
 -exec-next-instruction [--reverse]
```

:::

Executes one machine instruction. If the instruction is a function call, continues until the function returns. If the program stops at an instruction in the middle of a source line, the address will be printed as well.

If the '`--reverse`' option is specified, resumes reverse execution of the inferior program, stopping at the previous instruction. If the previously executed instruction was a return from another function, it will continue to execute in reverse until the call to that function (from the current stack frame) is reached.

#### [GDB]

The corresponding [GDB]'.

#### Example

::: smallexample

```bash
(gdb)
-exec-next-instruction
^running

(gdb)
*stopped,reason="end-stepping-range",
addr="0x000100d4",line="5",file="hello.c"
(gdb)
```

:::

#### The `-exec-return` Command

#### Synopsis

::: smallexample

```bash
 -exec-return
```

:::

Makes current function return immediately. Doesn't execute the inferior. Displays the new current frame.

#### [GDB]

The corresponding [GDB]'.

#### Example

::: smallexample

```bash
(gdb)
200-break-insert callee4
200^done,bkpt={number="1",addr="0x00010734",
file="../../../devo/gdb/testsuite/gdb.mi/basics.c",line="8"}
(gdb)
000-exec-run
000^running
(gdb)
000*stopped,reason="breakpoint-hit",disp="keep",bkptno="1",
frame={func="callee4",args=,
file="../../../devo/gdb/testsuite/gdb.mi/basics.c",
fullname="/home/foo/bar/devo/gdb/testsuite/gdb.mi/basics.c",line="8",
arch="i386:x86_64"}
(gdb)
205-break-delete
205^done
(gdb)
111-exec-return
111^done,frame={level="0",func="callee3",
args=[{name="strarg",
value="0x11940 \"A string argument.\""}],
file="../../../devo/gdb/testsuite/gdb.mi/basics.c",
fullname="/home/foo/bar/devo/gdb/testsuite/gdb.mi/basics.c",line="18",
arch="i386:x86_64"}
(gdb)
```

:::

#### The `-exec-run` Command

#### Synopsis

::: smallexample

```bash
 -exec-run [ --all | --thread-group N ] [ --start ]
```

:::

Starts execution of the inferior from the beginning. The inferior executes until either a breakpoint is encountered or the program exits. In the latter case the output will include an exit code, if the program has exited exceptionally.

When neither the '`--all`' option is specified, then all inferiors will be started.

Using the '`--start`' option instructs the debugger to stop the execution at the start of the inferior's main subprogram, following the same behavior as the `start` command (see [Starting](Starting.html#Starting)).

#### [GDB]

The corresponding [GDB]'.

#### Examples

::: smallexample

```bash
(gdb)
-break-insert main
^done,bkpt=
(gdb)
-exec-run
^running
(gdb)
*stopped,reason="breakpoint-hit",disp="keep",bkptno="1",
frame={func="main",args=,file="recursive2.c",
fullname="/home/foo/bar/recursive2.c",line="4",arch="i386:x86_64"}
(gdb)
```

:::

Program exited normally:

::: smallexample

```bash
(gdb)
-exec-run
^running
(gdb)
x = 55
*stopped,reason="exited-normally"
(gdb)
```

:::

Program exited exceptionally:

::: smallexample

```bash
(gdb)
-exec-run
^running
(gdb)
x = 55
*stopped,reason="exited",exit-code="01"
(gdb)
```

:::

Another way the program can terminate is if it receives a signal such as `SIGINT`. In this case, [GDB/MI] displays this:

::: smallexample

```bash
(gdb)
*stopped,reason="exited-signalled",signal-name="SIGINT",
signal-meaning="Interrupt"
```

:::

#### The `-exec-step` Command

#### Synopsis

::: smallexample

```bash
 -exec-step [--reverse]
```

:::

Resumes execution of the inferior program, stopping when the beginning of the next source line is reached, if the next source line is not a function call. If it is, stop at the first instruction of the called function. If the '`--reverse`' option is specified, resumes reverse execution of the inferior program, stopping at the beginning of the previously executed source line.

#### [GDB]

The corresponding [GDB]'.

#### Example

Stepping into a function:

::: smallexample

```bash
-exec-step
^running
(gdb)
*stopped,reason="end-stepping-range",
frame=,
],file="recursive2.c",
fullname="/home/foo/bar/recursive2.c",line="11",arch="i386:x86_64"}
(gdb)
```

:::

Regular stepping:

::: smallexample

```bash
-exec-step
^running
(gdb)
*stopped,reason="end-stepping-range",line="14",file="recursive2.c"
(gdb)
```

:::

#### The `-exec-step-instruction` Command

#### Synopsis

::: smallexample

```bash
 -exec-step-instruction [--reverse]
```

:::

Resumes the inferior which executes one machine instruction. If the '`--reverse` has stopped, will vary depending on whether we have stopped in the middle of a source line or not. In the former case, the address at which the program stopped will be printed as well.

#### [GDB]

The corresponding [GDB]'.

#### Example

::: smallexample

```bash
(gdb)
-exec-step-instruction
^running

(gdb)
*stopped,reason="end-stepping-range",
frame={func="foo",args=,file="try.c",
fullname="/home/foo/bar/try.c",line="10",arch="i386:x86_64"}
(gdb)
-exec-step-instruction
^running

(gdb)
*stopped,reason="end-stepping-range",
frame={addr="0x000100f4",func="foo",args=,file="try.c",
fullname="/home/foo/bar/try.c",line="10",arch="i386:x86_64"}
(gdb)
```

:::

#### The `-exec-until` Command

#### Synopsis

::: smallexample

```bash
 -exec-until [ locspec ]
```

:::

Executes the inferior until it reaches the address to which `locspec`'.

#### [GDB]

The corresponding [GDB]'.

#### Example

::: smallexample

```bash
(gdb)
-exec-until recursive2.c:6
^running
(gdb)
x = 55
*stopped,reason="location-reached",frame={func="main",args=,
file="recursive2.c",fullname="/home/foo/bar/recursive2.c",line="6",
arch="i386:x86_64"}
(gdb)
```

:::

---

::: header
Next: [GDB/MI Stack Manipulation](GDB_002fMI-Stack-Manipulation.html#GDB_002fMI-Stack-Manipulation)]
:::
