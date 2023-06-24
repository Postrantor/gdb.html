---
tip: translate by openai@2023-06-24 01:22:51
...
---
description: Process Record and Replay (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Process Record and Replay (Debugging with GDB)
lang: en
resource-type: document
title: Process Record and Replay (Debugging with GDB)
---
::: header
Next: [Stack](Stack.html#Stack)]
:::

---

## 7 Recording Inferior's Execution and Replaying It


On some platforms, [GDB] provides a special *process record and replay* target that can record a log of the process execution, and replay it later with both forward and reverse execution commands.

> 在某些平台上，GDB提供了一个特殊的进程记录和重放目标，可以记录进程执行的日志，并且可以使用前进和后退执行命令对其进行重放。


When this target is in use, if the execution log includes the record for the next instruction, [GDB] will debug in *replay mode*. In the replay mode, the inferior does not really execute code instructions. Instead, all the events that normally happen during code execution are taken from the execution log. While code is not really executed in replay mode, the values of registers (including the program counter register) and the memory of the inferior are still changed as they normally would. Their contents are taken from the execution log.

> 当使用此目标时，如果执行日志包括下一条指令的记录，[GDB]将以*回放模式*进行调试。 在回放模式下，下级实际上不会执行代码指令。 相反，所有通常在代码执行期间发生的事件都来自执行日志。 尽管代码实际上没有在回放模式下执行，但寄存器（包括程序计数器寄存器）和下级的内存仍然会按正常方式更改。 它们的内容来自执行日志。


If the record for the next instruction is not in the execution log, [GDB] records the execution log for future replay.

> 如果下一条指令的记录不在执行日志中，[GDB] 会记录执行日志以供将来重放。


The process record and replay target supports reverse execution (see [Reverse Execution](Reverse-Execution.html#Reverse-Execution)), even if the platform on which the inferior runs does not. However, the reverse execution is limited in this case by the range of the instructions recorded in the execution log. In other words, reverse execution on platforms that don't support it directly can only be done in the replay mode.

> 这种记录和重放目标支持反向执行（参见[反向执行](Reverse-Execution.html#Reverse-Execution)），即使下级运行的平台不支持也是如此。然而，在这种情况下，反向执行受到执行日志记录的指令范围的限制。换句话说，不支持反向执行的平台只能在重放模式下进行反向执行。


When debugging in the reverse direction, [GDB] will work in replay mode as long as the execution log includes the record for the previous instruction; otherwise, it will work in record mode, if the platform supports reverse execution, or stop if not.

> 当在反向调试时，如果执行日志包含前一条指令的记录，[GDB]将以回放模式工作；否则，如果平台支持反向执行，它将以记录模式工作，如果不支持，则停止。


Currently, process record and replay is supported on ARM, Aarch64, Moxie, PowerPC, PowerPC64, S/390, and x86 (i386/amd64) running GNU/Linux. Process record and replay can be used both when native debugging, and when remote debugging via `gdbserver`.

> 目前，ARM、Aarch64、Moxie、PowerPC、PowerPC64、S/390和x86（i386/amd64）运行的GNU/Linux都支持进程记录和重放功能。无论是本地调试还是通过“gdbserver”进行远程调试，都可以使用进程记录和重放功能。


For architecture environments that support process record and replay, [GDB] provides the following commands:

> 对于支持进程记录和重放的架构环境，[GDB]提供以下命令：

`record method`


This command starts the process record and replay target. The recording method can be specified as parameter. Without a parameter the command uses the `full` recording method. The following recording methods are available:

> 这个命令启动过程记录和重放目标。记录方法可以指定为参数。如果没有参数，则该命令使用“完整”记录方法。可用的记录方法有：

`full`


:   Full record/replay recording using [GDB]'s software record and replay implementation. This method allows replaying and reverse execution.

> 使用GDB的软件录制和回放实现完整记录/回放录制。此方法允许重放和反向执行。

`btrace format`


:   Hardware-supported instruction recording, supported on Intel processors. This method does not record data. Further, the data is collected in a ring buffer so old data will be overwritten when the buffer is full. It allows limited reverse execution. Variables and registers are not available during reverse execution. In remote debugging, recording continues on disconnect. Recorded data can be inspected after reconnecting. The recording may be stopped using `record stop`.

> 支持Intel处理器的硬件指令记录，此方法不记录数据。此外，数据存储在环形缓冲区中，因此当缓冲区满时，旧数据将被覆盖。它允许有限的反向执行。反向执行期间不可使用变量和寄存器。在远程调试期间，记录会继续，断开后可以检查记录的数据。可以使用“record stop”停止记录。

```
The recording format can be specified as parameter. Without a parameter the command chooses the recording format. The following recording formats are available:

`bts`

:   

    Use the *Branch Trace Store* (BTS) recording format. In this format, the processor stores a from/to record for each executed branch in the btrace ring buffer.

`pt`

:   

    Use the *Intel Processor Trace* recording format. In this format, the processor stores the execution trace in a compressed form that is afterwards decoded by [GDB].

    The trace can be recorded with very low overhead. The compressed trace format also allows small trace buffers to already contain a big number of instructions compared to BTS.

    Decoding the recorded execution trace, on the other hand, is more expensive than decoding BTS trace. This is mostly due to the increased number of instructions to process. You should increase the buffer-size with care.

Not all recording formats may be available on all processors.
```


The process record and replay target can only debug a process that is already running. Therefore, you need first to start the process with the [run] command.

> 过程记录和重放目标只能调试已经运行的进程。因此，您需要首先使用[运行]命令启动该进程。


Displaced stepping (see [displaced stepping](Maintenance-Commands.html#Maintenance-Commands)) will be automatically disabled when process record and replay target is started. That's because the process record and replay target doesn't support displaced stepping.

> 当启动进程记录和重放目标时，被替换的步进（参见[被替换的步进](Maintenance-Commands.html#Maintenance-Commands)）将被自动禁用。这是因为进程记录和重放目标不支持被替换的步进。


If the inferior is in the non-stop mode (see [Non-Stop Mode](Non_002dStop-Mode.html#Non_002dStop-Mode)) or in the asynchronous execution mode (see [Background Execution](Background-Execution.html#Background-Execution)), not all recording methods are available. The `full` recording method does not support these two modes.

> 如果在非停止模式（参见[非停止模式](Non_002dStop-Mode.html#Non_002dStop-Mode))或异步执行模式（参见[后台执行](Background-Execution.html#Background-Execution)）下，并不是所有的记录方法都可用。`full`记录方法不支持这两种模式。

`record stop`


Stop the process record and replay target. When process record and replay target stops, the entire execution log will be deleted and the inferior will either be terminated, or will remain in its final state.

> 停止进程记录和重放的目标。当进程记录和重放目标停止时，整个执行日志将被删除，下级将被终止，或者将保持其最终状态。


When you stop the process record and replay target in record mode (at the end of the execution log), the inferior will be stopped at the next instruction that would have been recorded. In other words, if you record for a while and then stop recording, the inferior process will be left in the same state as if the recording never happened.

> 当您停止进程记录和回放目标处于记录模式（在执行日志的末尾）时，次要程序将在下一条将被记录的指令处停止。换句话说，如果您记录一段时间然后停止记录，次要进程将处于与记录从未发生过相同的状态。


On the other hand, if the process record and replay target is stopped while in replay mode (that is, not at the end of the execution log, but at some earlier point), the inferior process will become "live" at that earlier state, and it will then be possible to continue the usual "live" debugging of the process from that state.

> 另一方面，如果在回放模式（即不是在执行日志的结尾，而是在某个较早的点）停止进程记录和回放目标，则劣势进程将在较早的状态“活跃”，然后就可以从该状态继续进行通常的“实时”调试进程。


When the inferior process exits, or [GDB] detaches from it, process record and replay target will automatically stop itself.

> 当下级进程退出或GDB与其分离时，进程记录和重放目标将自动停止。

`record goto`


Go to a specific location in the execution log. There are several ways to specify the location to go to:

> 在执行日志中转到特定位置。有几种方式指定要转到的位置：

`record goto begin`
`record goto start`

:   Go to the beginning of the execution log.

`record goto end`

:   Go to the end of the execution log.

`record goto n`

:   Go to instruction number `n` in the execution log.

`record save filename`


Save the execution log to a file `filename` is the process ID of the inferior.

> 将执行日志保存到文件`filename`是下级进程的进程ID。

This command may not be available for all recording methods.

`record restore filename`


Restore the execution log from a file `filename`. File must have been created with `record save`.

> 从文件`filename`恢复执行日志。文件必须是使用`record save`创建的。

`set record full insn-number-max limit`

`set record full insn-number-max unlimited`


Set the limit of instructions to be recorded for the `full` recording method. Default value is 200000.

> 设置`全部`录制方法要记录的指令的限制。默认值为200000。


If `limit` lets you control what happens when the limit is reached, by means of the `stop-at-limit` option, described below.)

> 如果`limit`可以通过下面描述的`stop-at-limit`选项来控制达到限制时发生的情况，那么它就可以帮助您控制。


If `limit` will never delete recorded instructions from the execution log. The number of recorded instructions is limited only by the available memory.

> 如果`限制`永远不会从执行日志中删除记录的指令，则记录的指令数量仅受可用内存的限制。

`show record full insn-number-max`


Show the limit of instructions to be recorded with the `full` recording method.

> 显示使用“完全”记录方法记录的指令的限制。

`set record full stop-at-limit`


Control the behavior of the `full` recording method when the number of recorded instructions reaches the limit. If ON (the default), [GDB] will stop when the limit is reached for the first time and ask you whether you want to stop the inferior or continue running it and recording the execution log. If you decide to continue recording, each new recorded instruction will cause the oldest one to be deleted.

> 当记录指令数达到限制时控制`full`记录方法的行为。如果开启（默认），[GDB]在首次达到限制时将停止，并询问您是否要停止下属进程或继续运行它并记录执行日志。如果您决定继续记录，每个新记录的指令将导致最旧的指令被删除。


If this option is OFF, [GDB] will automatically delete the oldest record to make room for each new one, without asking.

> 如果此选项关闭，[GDB]将自动删除最旧的记录，以便为每个新记录腾出空间，而无需询问。

`show record full stop-at-limit`

Show the current setting of `stop-at-limit`.

`set record full memory-query`


Control the behavior when [GDB] will query whether to stop the inferior in that case.

> 控制当[GDB]在这种情况下查询是否停止下级行为的行为。


If this option is OFF (the default), [GDB] replays this execution log, it will mark the log of this instruction as not accessible, and it will not affect the replay results.

> 如果这个选项是关闭的（默认情况下），[GDB]会重放这个执行日志，它会将这条指令的日志标记为不可访问，不会影响重放的结果。

`show record full memory-query`

Show the current setting of `memory-query`.


The `btrace` record target does not trace data. As a convenience, when replaying, [GDB] reads read-only memory off the live program directly, assuming that the addresses of the read-only areas don't change. This for example makes it possible to disassemble code while replaying, but not to print variables. In some cases, being able to inspect variables might be useful. You can use the following command for that:

> `btrace`记录目标不跟踪数据。为了方便起见，在重放时，[GDB]直接从实时程序中读取只读内存，假设只读区域的地址不会改变。这例如使得在重放时可以反汇编代码，但是不能打印变量。在某些情况下，能够检查变量可能是有用的。您可以使用以下命令来实现：

`set record btrace replay-memory-access`


Control the behavior of the `btrace` recording method when accessing memory during replay. If `read-only` (the default), [GDB] will allow accesses to read-only and to read-write memory. Beware that the accessed memory corresponds to the live target and not necessarily to the current replay position.

> 控制`btrace`记录方法在回放期间访问内存时的行为。如果是`只读`（默认），[GDB]将允许访问只读和读写内存。请注意，访问的内存对应于实时目标，而不一定对应于当前的回放位置。

`set record btrace cpu identifier`


Set the processor to be used for enabling workarounds for processor errata when decoding the trace.

> 设置处理器以用于解码跟踪时启用处理器错误的工作程序。


Processor errata are defects in processor operation, caused by its design or manufacture. They can cause a trace not to match the specification. This, in turn, may cause trace decode to fail. [GDB] can detect erroneous trace packets and correct them, thus avoiding the decoding failures. These corrections are known as *errata workarounds*, and are enabled based on the processor on which the trace was recorded.

> 处理器错误是由设计或制造引起的处理器操作中的缺陷。它们可能导致跟踪不符合规范。这反过来可能导致跟踪解码失败。[GDB]可以检测错误的跟踪数据包并进行纠正，从而避免解码失败。这些纠正被称为“错误工作程序”，并根据记录跟踪的处理器启用。


By default, [GDB] does not yet support it. This command allows you to do that, and also allows to disable the workarounds.

> 默认情况下，[GDB]尚不支持它。此命令允许您执行此操作，并允许禁用回避措施。


The argument `identifier` and is of the form: `vendor:processor identifier`. In addition, there are two special identifiers, `none` and `auto` (default).

> 参数`标识符`的格式为`vendor:processor identifier`。此外，还有两个特殊标识符，`none`和`auto`（默认）。


The following vendor identifiers and corresponding processor identifiers are currently supported:

> 以下供应商标识符和相应的处理器标识符当前受支持：

---

`intel`   `family`]

---


On GNU/Linux systems, the processor `family` can be obtained from `/proc/cpuinfo`.

> 在GNU/Linux系统中，可以从/proc/cpuinfo中获取处理器家族信息。

If `identifier` is `none`, errata workarounds are disabled.

For example, when using an old [GDB] supports.

::: smallexample

```bash
(gdb) info record
Active record target: record-btrace
Recording format: Intel Processor Trace.
Buffer size: 16kB.
Failed to configure the Intel Processor Trace decoder: unknown cpu.
(gdb) set record btrace cpu intel:6/158
(gdb) info record
Active record target: record-btrace
Recording format: Intel Processor Trace.
Buffer size: 16kB.
Recorded 84872 instructions in 3189 functions (0 gaps) for thread 1 (...).
```

:::

`show record btrace replay-memory-access`

Show the current setting of `replay-memory-access`.

`show record btrace cpu`


Show the processor to be used for enabling trace decode errata workarounds.

> 请展示用于启用跟踪解码错误工作绕过的处理器。

`set record btrace bts buffer-size size`

`set record btrace bts buffer-size unlimited`


Set the requested ring buffer size for branch tracing in BTS format. Default is 64KB.

> 设置BTS格式的请求环形缓冲区大小用于分支跟踪。默认是64KB。


If `size`. Use the `info record` command to see the actual buffer size for each thread that uses the btrace recording method and the BTS format.

> 如果使用btrace记录方法和BTS格式的每个线程的实际缓冲区大小，请使用`info record`命令查看。

If `limit` will try to allocate a buffer of 4MB.


Bigger buffers mean longer traces. On the other hand, [GDB] will also need longer to process the branch trace data before it can be used.

> 更大的缓冲区意味着更长的跟踪。另一方面，[GDB]在使用分支跟踪数据之前也需要更长的时间来处理。

`show record btrace bts buffer-size size`


Show the current setting of the requested ring buffer size for branch tracing in BTS format.

> 显示BTS格式中所请求的环形缓冲区大小的当前设置。

`set record btrace pt buffer-size size`

`set record btrace pt buffer-size unlimited`


Set the requested ring buffer size for branch tracing in Intel Processor Trace format. Default is 16KB.

> 设置Intel处理器跟踪格式的所请求的环形缓冲区大小。默认为16KB。


If `size`. Use the `info record` command to see the actual buffer size for each thread.

> 如果要查看每个线程的实际缓冲区大小，请使用`info record`命令。

If `limit` will try to allocate a buffer of 4MB.


Bigger buffers mean longer traces. On the other hand, [GDB] will also need longer to process the branch trace data before it can be used.

> 更大的缓冲区意味着更长的跟踪。另一方面，[GDB]在处理分支跟踪数据之前也需要更长的时间才能使用它。

`show record btrace pt buffer-size size`


Show the current setting of the requested ring buffer size for branch tracing in Intel Processor Trace format.

> 显示Intel处理器跟踪格式中所请求的环形缓冲区大小的当前设置。

`info record`


Show various statistics about the recording depending on the recording method:

> 显示根据录制方法的各种统计信息：

`full`


:   For the `full` recording method, it shows the state of process record and its in-memory execution log buffer, including:

> 对于完整的录制方法，它显示进程记录的状态及其内存中的执行日志缓冲区，包括：

```
-   Whether in record mode or replay mode.
-   Lowest recorded instruction number (counting from when the current execution log started recording instructions).
-   Highest recorded instruction number.
-   Current instruction about to be replayed (if in replay mode).
-   Number of instructions contained in the execution log.
-   Maximum number of instructions that may be contained in the execution log.
```

`btrace`

:   For the `btrace` recording method, it shows:

```
-   Recording format.
-   Number of instructions that have been recorded.
-   Number of blocks of sequential control-flow formed by the recorded instructions.
-   Whether in record mode or replay mode.

For the `bts` recording format, it also shows:

-   Size of the perf ring buffer.

For the `pt` recording format, it also shows:

-   Size of the perf ring buffer.
```

`record delete`


When record target runs in replay mode ("in the past"), delete the subsequent execution log and begin to record a new execution log starting from the current address. This means you will abandon the previously recorded "future" and begin recording a new "future".

> 当记录目标在回放模式（“过去”）中运行时，删除后续执行日志，并从当前地址开始记录新的执行日志。这意味着您将放弃先前记录的“未来”，并开始记录新的“未来”。

`record instruction-history`


Disassembles instructions from the recorded execution log. By default, ten instructions are disassembled. This can be changed using the `set record instruction-history-size` command. Instructions are printed in execution order.

> 从记录的执行日志中反汇编指令。默认情况下，将反汇编十条指令。可以使用`set record instruction-history-size`命令更改此设置。指令按执行顺序打印。


It can also print mixed source+disassembly if you specify the the `/m` or `/s` modifier, and print the raw instructions in hex as well as in symbolic form by specifying the `/r` or `/b` modifier. The behaviour of the `/m`, `/s`, `/r`, and `/b` modifiers are the same as for the [disassemble]](Machine-Code.html#disassemble)).

> 它也可以打印混合源码+反汇编，如果指定`/m`或`/s`修饰符，并以`/r`或`/b`修饰符的形式打印原始指令的十六进制和符号形式。`/m`、`/s`、`/r`和`/b`修饰符的行为与[反汇编](Machine-Code.html#disassemble))相同。


The current position marker is printed for the instruction at the current program counter value. This instruction can appear multiple times in the trace and the current position marker will be printed every time. To omit the current position marker, specify the `/p` modifier.

> 当前位置标记器是根据当前程序计数器的值打印出来的指令。这条指令可以在跟踪中多次出现，每次都会打印出当前位置标记器。要省略当前位置标记器，请指定`/p`修饰符。


To better align the printed instructions when the trace contains instructions from more than one function, the function name may be omitted by specifying the `/f` modifier.

> 为了更好地对齐包含来自多个函数的指令的打印指令，可以通过指定'/f'修饰符来省略函数名。


Speculatively executed instructions are prefixed with '`?`'. This feature is not available for all recording formats.

> 推测执行的指令前面会加上'`?`'。这个功能不适用于所有的录制格式。


There are several ways to specify what part of the execution log to disassemble:

> 有几种方法可以指定要反汇编的执行日志的哪一部分：

`record instruction-history insn`


:   Disassembles ten instructions starting from instruction number `insn`.

> 从指令号insn开始，反汇编十条指令。

`record instruction-history insn, +/-n`

:   Disassembles `n`.

`record instruction-history`

:   Disassembles ten more instructions after the last disassembly.

`record instruction-history -`

:   Disassembles ten more instructions before the last disassembly.

`record instruction-history begin, end`


:   Disassembles instructions beginning with instruction number `begin` is included.

> 解码从指令号 `begin` 开始的指令。

This command may not be available for all recording methods.

`set record instruction-history-size size`

`set record instruction-history-size unlimited`


Define how many instructions to disassemble in the `record instruction-history` command. The default value is 10. A `size` of `unlimited` means unlimited instructions.

> `record instruction-history`命令可以定义多少条指令进行反汇编。默认值为10。`size`设置为`unlimited`意味着无限多条指令。

`show record instruction-history-size`


Show how many instructions to disassemble in the `record instruction-history` command.

> 记录指令历史命令中要反汇编的指令数量有多少？

`record function-call-history`


Prints the execution history at function granularity. For each sequence of instructions that belong to the same function, it prints the name of that function, the source lines for this instruction sequence (if the `/l` modifier is specified), and the instructions numbers that form the sequence (if the `/i` modifier is specified). The function names are indented to reflect the call stack depth if the `/c` modifier is specified. The `/l`, `/i`, and `/c` modifiers can be given together.

> 打印函数粒度的执行历史记录。对于属于同一函数的每个指令序列，它会打印该函数的名称、此指令序列的源行（如果指定了“/l”修饰符），以及组成该序列的指令号（如果指定了“/i”修饰符）。如果指定了“/c”修饰符，则函数名称会缩进以反映调用堆栈深度。可以同时指定“/l”、“/i”和“/c”修饰符。

::: smallexample

```bash
(gdb) list 1, 10
1   void foo (void)
2   {
3   }
4
5   void bar (void)
6   {
7     ...
8     foo ();
9     ...
10  }
(gdb) record function-call-history /ilc
1  bar     inst 1,4     at foo.c:6,8
2    foo   inst 5,10    at foo.c:2,3
3  bar     inst 11,13   at foo.c:9,10
```

:::


By default, ten functions are printed. This can be changed using the `set record function-call-history-size` command. Functions are printed in execution order. There are several ways to specify what to print:

> 默认情况下，会打印十个函数。可以使用`set record function-call-history-size`命令来更改这个数量。函数会按照执行顺序打印出来。有几种方法可以指定要打印的内容：

`record function-call-history func`

:   Prints ten functions starting from function number `func`.

`record function-call-history func, +/-n`

:   Prints `n`.

`record function-call-history`

:   Prints ten more functions after the last ten-function print.

`record function-call-history -`

:   Prints ten more functions before the last ten-function print.

`record function-call-history begin, end`

:   Prints functions beginning with function number `begin` is included.

This command may not be available for all recording methods.

`set record function-call-history-size size`

`set record function-call-history-size unlimited`


Define how many functions to print in the `record function-call-history` command. The default value is 10. A size of `unlimited` means unlimited functions.

> 定义`record function-call-history`命令要打印多少个函数。默认值是10。`unlimited`的大小意味着无限的功能。

`show record function-call-history-size`


Show how many functions to print in the `record function-call-history` command.

> 请告诉我们在`record function-call-history`命令中要打印多少个功能。

---

::: header
Next: [Stack](Stack.html#Stack)]
:::
