---
tip: translate by openai@2023-06-23 22:06:05
...
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

> 这些是异步命令，它们只有在远程目标上才会生成“stopped”的超带记录，而在其他情况下，这种交互也会被模拟。

#### The `-exec-continue` Command

#### Synopsis

::: smallexample

```bash
 -exec-continue [--reverse] [--all|--thread-group N]
```

:::


Resumes the execution of the inferior program, which will continue to execute until it reaches a debugger stop event. If the '`--reverse`' option is specified, execution resumes in reverse until it reaches a stop event. Stop events may include

> 恢复下级程序的执行，该程序将继续执行直到遇到调试器停止事件。 如果指定了'--reverse'选项，则以相反顺序执行，直到遇到停止事件。 停止事件可能包括

- breakpoints or watchpoints
- signals or exceptions
- the end of the process (or its beginning under '`--reverse`')
- the end or beginning of a replay log if one is being used.


In all-stop mode (see [All-Stop Mode](All_002dStop-Mode.html#All_002dStop-Mode)), may resume only one thread, or all threads, depending on the value of the '`scheduler-locking`' options is specified, then all threads in that thread group are resumed.

> 在全停止模式（参见[全停止模式](All_002dStop-Mode.html#All_002dStop-Mode)）中，可以根据'`scheduler-locking`'选项的值恢复一个线程或所有线程，然后恢复该线程组中的所有线程。

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

> 恢复执行下级程序，直到当前函数退出。显示函数返回的结果。如果指定了'--reverse'选项，则恢复反向执行下级程序，直到调用当前函数的位置。

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

> 函数返回除`void`之外的值。内部[GDB]变量存储结果的名称和值本身一起被打印出来。

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

> 打断目标的后台执行。注意，与停止消息关联的令牌是已被中断的执行命令的令牌。中断本身的令牌只出现在“^done”输出中。如果用户试图中断一个未运行的程序，将打印出错误消息。


Note that when asynchronous execution is enabled, this command is asynchronous just like other execution commands. That is, first the '`^done`' notification.

> 注意，当启用异步执行时，此命令与其他执行命令一样是异步的。也就是说，首先是“^done”通知。


In non-stop mode, only the context thread is interrupted by default. All threads (in all inferiors) will be interrupted if the '`--all`' option is specified, all threads in that group will be interrupted.

> 在不间断模式下，默认只中断上下文线程。如果指定'--all'选项，则会中断该组中的所有线程。

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

> 恢复在locspec指定地址处的下级程序的执行。

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

> 恢复执行下级程序，在到达下一行源代码开头时停止。


If the '`--reverse`' option is specified, resumes reverse execution of the inferior program, stopping at the beginning of the previous source line. If you issue this command on the first line of a function, it will take you back to the caller of that function, to the source line where the function was called.

> 如果指定了'--reverse'选项，则恢复反向执行下级程序，在前一源行的开头停止。如果您在函数的第一行发出此命令，它将带您回到调用该函数的调用者，到调用函数的源行。

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

> 执行一条机器指令。如果指令是函数调用，则继续执行直到函数返回。如果程序在源代码行中间的指令处停止，也会打印地址。


If the '`--reverse`' option is specified, resumes reverse execution of the inferior program, stopping at the previous instruction. If the previously executed instruction was a return from another function, it will continue to execute in reverse until the call to that function (from the current stack frame) is reached.

> 如果指定了'--reverse'选项，则会恢复对次级程序的反向执行，并在上一条指令处停止。如果先前执行的指令是从另一个函数返回，它将继续反向执行，直到到达从当前堆栈帧调用该函数的地方。

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

> 立即使当前函数返回，不执行下级函数。显示新的当前帧。

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

> 开始从头执行下级程序。下级程序会一直执行，直到遇到断点或者程序结束。在后者的情况下，输出将包括一个退出代码，如果程序异常退出的话。


When neither the '`--all`' option is specified, then all inferiors will be started.

> 如果没有指定'--all'选项，那么所有下属都会被启动。


Using the '`--start`' option instructs the debugger to stop the execution at the start of the inferior's main subprogram, following the same behavior as the `start` command (see [Starting](Starting.html#Starting)).

> 使用'--start'选项可以指示调试器在下级主程序开始处停止执行，行为与'start'命令相同（参见[开始](Starting.html#Starting)）。

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

> 程序的另一种终止方式是收到信号，例如`SIGINT`。在这种情况下，[GDB/MI]会显示：

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

> 恢复执行下级程序，如果下一个源行不是函数调用，则停止在下一个源行的开头。如果它是，则在被调用函数的第一条指令处停止。如果指定了“--reverse”选项，则恢复下级程序的反向执行，停在先前执行的源行的开头。

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

> 恢复执行单条机器指令的次级程序。如果'--reverse'已停止，则取决于我们是否停止在源代码行中间。在前一种情况下，程序停止的地址也将被打印出来。

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
