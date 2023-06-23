---
tip: translate by openai@2023-06-23 14:25:18
...
---
description: tfind (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: tfind (Debugging with GDB)
lang: en
resource-type: document
title: tfind (Debugging with GDB)
---------------------------------

::: header
Next: [tdump](tdump.html#tdump)]
:::

---

#### 13.2.1 `tfind n`

The basic command for selecting a trace snapshot from the buffer is `tfind n`, which finds trace snapshot number `n` is given, the next snapshot is selected.

> 基本命令用于从缓冲区中选择跟踪快照的命令是 `tfind n`，它会找到给定的跟踪快照编号 `n`，然后会选择下一个快照。

Here are the various forms of using the `tfind` command.

> 以下是使用 `tfind` 命令的各种形式。

`tfind start`

:   Find the first snapshot in the buffer. This is a synonym for `tfind 0` (since 0 is the number of the first snapshot).

> 找到缓冲区中的第一个快照。这是 `tfind 0` 的同义词（因为 0 是第一个快照的编号）。

`tfind none`

:   Stop debugging trace snapshots, resume *live* debugging.

> 停止调试跟踪快照，继续*实时*调试。

`tfind end`

:   Same as '`tfind none`'.

> 与 'tfind none' 相同。

`tfind`

:   No argument means find the next trace snapshot or find the first one if no trace snapshot is selected.

> 没有参数意味着查找下一个跟踪快照，如果没有选择跟踪快照，则查找第一个。

`tfind -`

:   Find the previous trace snapshot before the current one. This permits retracing earlier steps.

> 找到当前之前的跟踪快照。这样可以回溯到更早的步骤。

`tfind tracepoint num`

:   Find the next snapshot associated with tracepoint `num` is given, it means find the next snapshot collected for the same tracepoint as the current snapshot.

> 找到与追踪点 `num` 相关的下一个快照，这意味着找到与当前快照相同追踪点的下一个快照。

`tfind pc addr`

:   Find the next snapshot associated with the value `addr` is given, it means find the next snapshot with the same value of PC as the current snapshot.

> 找到与 `addr` 值相关的下一个快照，这意味着找到与当前快照 PC 值相同的下一个快照。

`tfind outside addr1, addr2`

:   Find the next snapshot whose PC is outside the given range of addresses (exclusive).

> 找出下一个 PC 地址超出给定范围（不包括）的快照。

`tfind range addr1, addr2`

:   Find the next snapshot whose PC is between `addr1` (inclusive).

> 找到下一个 PC 在 `addr1`（包含）之间的快照。

`tfind line [file:]n`

:   Find the next snapshot associated with the source line `n` is given, it means find the next line other than the one currently being examined; thus saying `tfind line` repeatedly can appear to have the same effect as stepping from line to line in a *live* debugging session.

> 找到与源代码行 `n` 相关联的下一个快照，这意味着找到当前正在检查的行之外的下一行；因此，重复地说 `tfind line` 似乎具有与*实时*调试会话中从一行到另一行一样的效果。

The default arguments for the `tfind` commands are specifically designed to make it easy to scan through the trace buffer. For instance, `tfind` with no argument selects the next trace snapshot, and `tfind -` with no argument selects the previous trace snapshot. So, by giving one `tfind` command, and then simply hitting RET repeatedly you can examine all the trace snapshots in order. Or, by saying `tfind -` and then hitting RET repeatedly you can examine the snapshots in reverse order. The `tfind line` command with no argument selects the snapshot for the next source line executed. The `tfind pc` command with no argument selects the next snapshot with the same program counter (PC) as the current frame. The `tfind tracepoint` command with no argument selects the next trace snapshot collected by the same tracepoint as the current one.

> 默认参数为 `tfind` 命令设计是为了让您轻松扫描跟踪缓冲区。例如，不带参数的 `tfind` 会选择下一个跟踪快照，而不带参数的 `tfind -` 则会选择上一个跟踪快照。因此，只需给出一个 `tfind` 命令，然后反复按回车键就可以按顺序检查所有跟踪快照。或者，通过输入 `tfind -` 然后反复按回车键，您可以按相反的顺序检查快照。不带参数的 `tfind line` 命令会选择下一个要执行的源代码行的快照。不带参数的 `tfind pc` 命令会选择与当前帧具有相同程序计数器（PC）的下一个快照。不带参数的 `tfind tracepoint` 命令会选择与当前快照由同一跟踪点收集的下一个快照。

In addition to letting you scan through the trace buffer manually, these commands make it easy to construct [GDB] scripts that scan through the trace buffer and print out whatever collected data you are interested in. Thus, if we want to examine the PC, FP, and SP registers from each trace frame in the buffer, we can say this:

> 此外，这些命令还可以让您手动扫描跟踪缓冲区，从而可以方便地构建[GDB]脚本，以扫描跟踪缓冲区并打印出您感兴趣的任何收集数据。因此，如果我们要检查缓冲区中每个跟踪帧的 PC，FP 和 SP 寄存器，我们可以这样说：

::: smallexample

```bash
(gdb) tfind start
(gdb) while ($trace_frame != -1)
> printf "Frame %d, PC = %08X, SP = %08X, FP = %08X\n", \
          $trace_frame, $pc, $sp, $fp
> tfind
> end

Frame 0, PC = 0020DC64, SP = 0030BF3C, FP = 0030BF44
Frame 1, PC = 0020DC6C, SP = 0030BF38, FP = 0030BF44
Frame 2, PC = 0020DC70, SP = 0030BF34, FP = 0030BF44
Frame 3, PC = 0020DC74, SP = 0030BF30, FP = 0030BF44
Frame 4, PC = 0020DC78, SP = 0030BF2C, FP = 0030BF44
Frame 5, PC = 0020DC7C, SP = 0030BF28, FP = 0030BF44
Frame 6, PC = 0020DC80, SP = 0030BF24, FP = 0030BF44
Frame 7, PC = 0020DC84, SP = 0030BF20, FP = 0030BF44
Frame 8, PC = 0020DC88, SP = 0030BF1C, FP = 0030BF44
Frame 9, PC = 0020DC8E, SP = 0030BF18, FP = 0030BF44
Frame 10, PC = 00203F6C, SP = 0030BE3C, FP = 0030BF14
```

:::

Or, if we want to examine the variable `X` at each source line in the buffer:

> 如果我们想在缓冲区的每个源行中检查变量 `X`：

::: smallexample

```bash
(gdb) tfind start
(gdb) while ($trace_frame != -1)
> printf "Frame %d, X == %d\n", $trace_frame, X
> tfind line
> end

Frame 0, X = 1
Frame 7, X = 2
Frame 13, X = 255
```

:::

---

::: header
Next: [tdump](tdump.html#tdump)]
:::
