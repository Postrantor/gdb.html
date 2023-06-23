---
tip: translate by openai@2023-06-23 13:28:57
...
---
description: Starting and Stopping Trace Experiments (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Starting and Stopping Trace Experiments (Debugging with GDB)
lang: en
resource-type: document
title: Starting and Stopping Trace Experiments (Debugging with GDB)
-------------------------------------------------------------------

::: header
Next: [Tracepoint Restrictions](Tracepoint-Restrictions.html#Tracepoint-Restrictions)]
:::

---

#### 13.1.9 Starting and Stopping Trace Experiments

`tstart`

This command starts the trace experiment, and begins collecting data. It has the side effect of discarding all the data collected in the trace buffer during the previous trace experiment. If any arguments are supplied, they are taken as a note and stored with the trace experiment's state. The notes may be arbitrary text, and are especially useful with disconnected tracing in a multi-user context; the notes can explain what the trace is doing, supply user contact information, and so forth.

> 这个命令启动跟踪实验，并开始收集数据。它会副作用地丢弃在上一个跟踪实验期间缓冲区中收集的所有数据。如果提供了任何参数，它们将被视为注释并存储在跟踪实验的状态中。注释可以是任意文本，尤其在多用户环境中的断开跟踪中很有用；注释可以解释跟踪正在做什么，提供用户联系信息等等。

`tstop`

This command stops the trace experiment. If any arguments are supplied, they are recorded with the experiment as a note. This is useful if you are stopping a trace started by someone else, for instance if the trace is interfering with the system's behavior and needs to be stopped quickly.

> 这条命令停止跟踪实验。如果提供了任何参数，它们将与实验一起记录为一个注释。如果您停止了别人开始的跟踪，这是非常有用的，例如，如果跟踪干扰系统的行为，需要迅速停止。

**Note**: a trace experiment and data collection may stop automatically if any tracepoint's passcount is reached (see [Tracepoint Passcounts](Tracepoint-Passcounts.html#Tracepoint-Passcounts)), or if the trace buffer becomes full.

> **注意**：如果任何跟踪点的通过次数达到（参见[跟踪点通过次数]（Tracepoint-Passcounts.html#Tracepoint-Passcounts）），或者跟踪缓冲区已满，则跟踪实验和数据采集可能会自动停止。

`tstatus`

This command displays the status of the current trace data collection.

> 这个命令显示当前跟踪数据收集的状态。

Here is an example of the commands we described so far:

> 这是我们到目前为止所描述的命令的一个例子：

::: smallexample

```bash
(gdb) trace gdb_c_test
(gdb) actions
Enter actions for tracepoint #1, one per line.
> collect $regs,$locals,$args
> while-stepping 11
  > collect $regs
  > end
> end
(gdb) tstart
    [time passes …]
(gdb) tstop
```

:::

You can choose to continue running the trace experiment even if [GDB].

> 你可以选择继续运行跟踪实验，即使是[GDB]。

`set disconnected-tracing on`
`set disconnected-tracing off`

:

```
Choose whether a tracing run should continue to run if [GDB] has disconnected from the target. Note that `detach` or `quit` will ask you directly what to do about a running trace no matter what this variable's setting, so the variable is mainly useful for handling unexpected situations, such as loss of the network.
```

`show disconnected-tracing`

:

```
Show the current choice for disconnected tracing.
```

When you reconnect to the target, the trace experiment may or may not still be running; it might have filled the trace buffer in the meantime, or stopped for one of the other reasons. If it is running, it will continue after reconnection.

> 当您重新连接到目标时，跟踪实验可能仍在运行，也可能已经在此期间填满了跟踪缓冲区或因其他原因而停止。如果它正在运行，重新连接后它将继续运行。

Upon reconnection, the target will upload information about the tracepoints in effect. [GDB], the debugger will create a new tracepoint, so that you have a number with which to specify that tracepoint. This matching-up process is necessarily heuristic, and it may result in useless tracepoints being created; you may simply delete them if they are of no use.

> 重新连接后，目标将上传有效跟踪点的信息。[GDB]调试器将创建一个新的跟踪点，以便您有一个号码来指定该跟踪点。这个匹配过程必须是启发式的，它可能会导致无用的跟踪点被创建；如果它们没有用，您可以直接删除它们。

If your target agent supports a *circular trace buffer*, then you can run a trace experiment indefinitely without filling the trace buffer; when space runs out, the agent deletes already-collected trace frames, oldest first, until there is enough room to continue collecting. This is especially useful if your tracepoints are being hit too often, and your trace gets terminated prematurely because the buffer is full. To ask for a circular trace buffer, simply set '`circular-trace-buffer`' to on. You can set this at any time, including during tracing; if the agent can do it, it will change buffer handling on the fly, otherwise it will not take effect until the next run.

> 如果你的目标代理支持一个*循环跟踪缓冲区*，那么你可以无限期地运行跟踪实验而无需填满跟踪缓冲区；当空间用完时，代理会删除已收集的跟踪帧，最早的先删，直到有足够的空间继续收集。如果你的跟踪点被触发的太频繁，你的跟踪会因缓冲区满而被过早终止，这就特别有用了。要请求循环跟踪缓冲区，只需将'`circular-trace-buffer`'设置为 on。你可以在任何时候设置它，包括在跟踪期间；如果代理可以做到，它会实时改变缓冲区处理，否则它不会生效，直到下一次运行。

`set circular-trace-buffer on`
`set circular-trace-buffer off`

:

```
Choose whether a tracing run should use a linear or circular buffer for trace data. A linear buffer will not lose any trace data, but may fill up prematurely, while a circular buffer will discard old trace data, but it will have always room for the latest tracepoint hits.
```

`show circular-trace-buffer`

:

```
Show the current choice for the trace buffer. Note that this may not match the agent's current buffer handling, nor is it guaranteed to match the setting that might have been in effect during a past run, for instance if you are looking at frames from a trace file.
```

```

```

`set trace-buffer-size n`
`set trace-buffer-size unlimited`

:

```
Request that the target use a trace buffer of `n` bytes. Not all targets will honor the request; they may have a compiled-in size for the trace buffer, or some other limitation. Set to a value of `unlimited` or `-1` to let the target use whatever size it likes. This is also the default.
```

`show trace-buffer-size`

:

```
Show the current requested size for the trace buffer. Note that this will only match the actual size if the target supports size-setting, and was able to handle the requested size. For instance, if the target can only change buffer size between runs, this variable will not reflect the change until the next run starts. Use `tstatus` to get a report of the actual buffer size.
```

```

```

| `set trace-user text` |
| :-------------------: |

| `show trace-user` |
| :---------------: |

`set trace-notes text`

:

```
Set the trace run's notes.
```

`show trace-notes`

:

```
Show the trace run's notes.
```

`set trace-stop-notes text`

:

```
Set the trace run's stop notes. The handling of the note is as for `tstop` arguments; the set command is convenient way to fix a stop note that is mistaken or incomplete.
```

`show trace-stop-notes`

:

```
Show the trace run's stop notes.
```

---

::: header
Next: [Tracepoint Restrictions](Tracepoint-Restrictions.html#Tracepoint-Restrictions)]
:::
