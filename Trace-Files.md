---
tip: translate by openai@2023-06-23 14:41:49
...
---
description: Trace Files (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Trace Files (Debugging with GDB)
lang: en
resource-type: document
title: Trace Files (Debugging with GDB)
---
::: header
Previous: [Tracepoint Variables](Tracepoint-Variables.html#Tracepoint-Variables)]
:::

---

### 13.4 Using Trace Files


In some situations, the target running a trace experiment may no longer be available; perhaps it crashed, or the hardware was needed for a different activity. To handle these cases, you can arrange to dump the trace data into a file, and later use that file as a source of trace data, via the `target tfile` command.

> 在某些情况下，运行跟踪实验的目标可能不再可用；也许它崩溃了，或者硬件被用于其他活动。为了处理这些情况，您可以安排将跟踪数据转储到文件中，然后稍后使用该文件作为跟踪数据的来源，通过`target tfile`命令。

`tsave [ -r ] filename`

`tsave [-ctf] dirname`


Save the trace data to `filename` in its own filesystem, which may be more efficient if the trace buffer is very large. (Note, however, that `target tfile` can only read from files accessible to the host.) By default, this command will save trace frame in tfile format. You can supply the optional argument `-ctf` to save data in CTF format. The *Common Trace Format* (CTF) is proposed as a trace format that can be shared by multiple debugging and tracing tools. Please go to '`http://www.efficios.com/ctf`' to get more information.

> 将跟踪数据保存到其自己的文件系统中的`文件名`中，如果跟踪缓冲区非常大，这可能更有效。（但是，请注意，`目标tfile`只能从主机可访问的文件中读取。）默认情况下，此命令将以tfile格式保存跟踪帧。您可以提供可选参数`-ctf`以CTF格式保存数据。*通用跟踪格式*（CTF）被提出作为可由多个调试和跟踪工具共享的跟踪格式。请访问'`http://www.efficios.com/ctf`'以获取更多信息。

`target tfile filename`

`target ctf dirname`


Use the file named `filename` must be on a filesystem accessible to the host.

> 使用名为“文件名”的文件必须位于主机可访问的文件系统中。

::: smallexample

```bash
(gdb) target ctf ctf.ctf
(gdb) tfind
Found trace frame 0, tracepoint 2
39            ++a;  /* set tracepoint 1 here */
(gdb) tdump
Data collected at tracepoint 2, trace frame 0:
i = 0
a = 0
b = 1 '\001'
c = 
d = 
(gdb) p b
$1 = 1
```

:::

---

::: header
Previous: [Tracepoint Variables](Tracepoint-Variables.html#Tracepoint-Variables)]
:::
