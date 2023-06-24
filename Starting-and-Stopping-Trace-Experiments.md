---
tip: translate by openai@2023-06-24 03:09:42
...
---
description: Starting and Stopping Trace Experiments (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Starting and Stopping Trace Experiments (Debugging with GDB)
lang: en
resource-type: document
title: Starting and Stopping Trace Experiments (Debugging with GDB)
---
::: header
Next: [Tracepoint Restrictions](Tracepoint-Restrictions.html#Tracepoint-Restrictions)]
:::

---

#### 13.1.9 Starting and Stopping Trace Experiments

`tstart`


This command starts the trace experiment, and begins collecting data. It has the side effect of discarding all the data collected in the trace buffer during the previous trace experiment. If any arguments are supplied, they are taken as a note and stored with the trace experiment's state. The notes may be arbitrary text, and are especially useful with disconnected tracing in a multi-user context; the notes can explain what the trace is doing, supply user contact information, and so forth.

> 这个命令启动跟踪实验，并开始收集数据。它会产生抛弃前一次跟踪实验中缓冲区中收集的所有数据的副作用。如果提供了任何参数，它们将被作为注释并存储在跟踪实验的状态中。注释可以是任意文本，在多用户上下文中进行断开跟踪时特别有用；注释可以解释跟踪在做什么，提供用户联系信息等等。

`tstop`


This command stops the trace experiment. If any arguments are supplied, they are recorded with the experiment as a note. This is useful if you are stopping a trace started by someone else, for instance if the trace is interfering with the system's behavior and needs to be stopped quickly.

> 这个命令停止跟踪实验。如果提供任何参数，它们将与实验一起记录为注释。如果您要停止其他人开始的跟踪，这很有用，例如如果跟踪干扰系统的行为并且需要迅速停止，则可以迅速停止。


**Note**: a trace experiment and data collection may stop automatically if any tracepoint's passcount is reached (see [Tracepoint Passcounts](Tracepoint-Passcounts.html#Tracepoint-Passcounts)), or if the trace buffer becomes full.

> **注意**：如果任何跟踪点的通过计数达到（参见[跟踪点通过计数]（Tracepoint-Passcounts.html#Tracepoint-Passcounts）），或者跟踪缓冲区已满，则跟踪实验和数据收集可能会自动停止。

`tstatus`

This command displays the status of the current trace data collection.

Here is an example of the commands we described so far:

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

> 当您重新连接到目标时，跟踪实验可能仍在运行，也可能在此期间已填满跟踪缓冲区或因其他原因停止。如果正在运行，则在重新连接后将继续运行。


Upon reconnection, the target will upload information about the tracepoints in effect. [GDB], the debugger will create a new tracepoint, so that you have a number with which to specify that tracepoint. This matching-up process is necessarily heuristic, and it may result in useless tracepoints being created; you may simply delete them if they are of no use.

> 重新连接后，目标将上传有效跟踪点的信息。[GDB]调试器将创建一个新的跟踪点，因此您有一个数字可以指定该跟踪点。这种匹配过程必然是启发式的，可能会导致创建无用的跟踪点；如果它们没有用，您可以直接删除它们。


If your target agent supports a *circular trace buffer*, then you can run a trace experiment indefinitely without filling the trace buffer; when space runs out, the agent deletes already-collected trace frames, oldest first, until there is enough room to continue collecting. This is especially useful if your tracepoints are being hit too often, and your trace gets terminated prematurely because the buffer is full. To ask for a circular trace buffer, simply set '`circular-trace-buffer`' to on. You can set this at any time, including during tracing; if the agent can do it, it will change buffer handling on the fly, otherwise it will not take effect until the next run.

> 如果目标代理支持*循环跟踪缓冲区*，那么您可以无限期地运行跟踪实验而不会填满跟踪缓冲区；当空间用尽时，代理会删除已收集的跟踪帧，从最旧的开始，直到有足够的空间继续收集。如果您的跟踪点被太频繁地触发，而且跟踪因缓冲区已满而被过早终止，这将特别有用。要请求循环跟踪缓冲区，只需将'`circular-trace-buffer`'设置为on即可。您可以随时设置此值，包括在跟踪期间；如果代理可以执行，它将即时更改缓冲区处理，否则它将不会在下一次运行时生效。

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
<!-- -->
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
<!-- -->
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
