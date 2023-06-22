---
description: tfind (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: tfind (Debugging with GDB)
lang: en
resource-type: document
title: tfind (Debugging with GDB)
---
::: header
Next: [tdump](tdump.html#tdump)]
:::

---

#### 13.2.1 `tfind n`

The basic command for selecting a trace snapshot from the buffer is `tfind n`, which finds trace snapshot number `n` is given, the next snapshot is selected.

Here are the various forms of using the `tfind` command.

`tfind start`

:   Find the first snapshot in the buffer. This is a synonym for `tfind 0` (since 0 is the number of the first snapshot).

`tfind none`

:   Stop debugging trace snapshots, resume *live* debugging.

`tfind end`

:   Same as '`tfind none`'.

`tfind`

:   No argument means find the next trace snapshot or find the first one if no trace snapshot is selected.

`tfind -`

:   Find the previous trace snapshot before the current one. This permits retracing earlier steps.

`tfind tracepoint num`

:   Find the next snapshot associated with tracepoint `num` is given, it means find the next snapshot collected for the same tracepoint as the current snapshot.

`tfind pc addr`

:   Find the next snapshot associated with the value `addr` is given, it means find the next snapshot with the same value of PC as the current snapshot.

`tfind outside addr1, addr2`

:   Find the next snapshot whose PC is outside the given range of addresses (exclusive).

`tfind range addr1, addr2`

:   Find the next snapshot whose PC is between `addr1` (inclusive).

`tfind line [file:]n`

:   Find the next snapshot associated with the source line `n` is given, it means find the next line other than the one currently being examined; thus saying `tfind line` repeatedly can appear to have the same effect as stepping from line to line in a *live* debugging session.

The default arguments for the `tfind` commands are specifically designed to make it easy to scan through the trace buffer. For instance, `tfind` with no argument selects the next trace snapshot, and `tfind -` with no argument selects the previous trace snapshot. So, by giving one `tfind` command, and then simply hitting RET repeatedly you can examine all the trace snapshots in order. Or, by saying `tfind -` and then hitting RET repeatedly you can examine the snapshots in reverse order. The `tfind line` command with no argument selects the snapshot for the next source line executed. The `tfind pc` command with no argument selects the next snapshot with the same program counter (PC) as the current frame. The `tfind tracepoint` command with no argument selects the next trace snapshot collected by the same tracepoint as the current one.

In addition to letting you scan through the trace buffer manually, these commands make it easy to construct [GDB] scripts that scan through the trace buffer and print out whatever collected data you are interested in. Thus, if we want to examine the PC, FP, and SP registers from each trace frame in the buffer, we can say this:

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
