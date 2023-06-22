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

`tsave [ -r ] filename`

`tsave [-ctf] dirname`

Save the trace data to `filename` in its own filesystem, which may be more efficient if the trace buffer is very large. (Note, however, that `target tfile` can only read from files accessible to the host.) By default, this command will save trace frame in tfile format. You can supply the optional argument `-ctf` to save data in CTF format. The *Common Trace Format* (CTF) is proposed as a trace format that can be shared by multiple debugging and tracing tools. Please go to '`http://www.efficios.com/ctf`' to get more information.

`target tfile filename`

`target ctf dirname`

Use the file named `filename` must be on a filesystem accessible to the host.

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
