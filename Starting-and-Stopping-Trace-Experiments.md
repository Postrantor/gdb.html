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

`tstop`

This command stops the trace experiment. If any arguments are supplied, they are recorded with the experiment as a note. This is useful if you are stopping a trace started by someone else, for instance if the trace is interfering with the system's behavior and needs to be stopped quickly.

**Note**: a trace experiment and data collection may stop automatically if any tracepoint's passcount is reached (see [Tracepoint Passcounts](Tracepoint-Passcounts.html#Tracepoint-Passcounts)), or if the trace buffer becomes full.

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

Upon reconnection, the target will upload information about the tracepoints in effect. [GDB], the debugger will create a new tracepoint, so that you have a number with which to specify that tracepoint. This matching-up process is necessarily heuristic, and it may result in useless tracepoints being created; you may simply delete them if they are of no use.

If your target agent supports a *circular trace buffer*, then you can run a trace experiment indefinitely without filling the trace buffer; when space runs out, the agent deletes already-collected trace frames, oldest first, until there is enough room to continue collecting. This is especially useful if your tracepoints are being hit too often, and your trace gets terminated prematurely because the buffer is full. To ask for a circular trace buffer, simply set '`circular-trace-buffer`' to on. You can set this at any time, including during tracing; if the agent can do it, it will change buffer handling on the fly, otherwise it will not take effect until the next run.

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
