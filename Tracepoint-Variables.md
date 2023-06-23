---
description: Tracepoint Variables (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Tracepoint Variables (Debugging with GDB)
lang: en
resource-type: document
title: Tracepoint Variables (Debugging with GDB)
---
::: header
Next: [Trace Files](Trace-Files.html#Trace-Files)]
:::

---

### 13.3 Convenience Variables for Tracepoints

`(int) $trace_frame`

The current trace snapshot (a.k.a. *frame*) number, or -1 if no snapshot is selected.

`(int) $tracepoint`

The tracepoint for the current trace snapshot.

`(int) $trace_line`

The line number for the current trace snapshot.

`(char ) $trace_file`

The source file for the current trace snapshot.

`(char ) $trace_func`

The name of the function containing `$tracepoint`.

Note: `$trace_file` is not suitable for use in `printf`, use `output` instead.

Here's a simple example of using these convenience variables for stepping through all the trace snapshots and printing some of their data. Note that these are not the same as trace state variables, which are managed by the target.

::: smallexample

```bash
(gdb) tfind start

(gdb) while $trace_frame != -1
> output $trace_file
> printf ", line %d (tracepoint #%d)\n", $trace_line, $tracepoint
> tfind
> end
```

:::
