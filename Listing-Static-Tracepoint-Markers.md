---
description: Listing Static Tracepoint Markers (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Listing Static Tracepoint Markers (Debugging with GDB)
lang: en
resource-type: document
title: Listing Static Tracepoint Markers (Debugging with GDB)
---
::: header
Next: [Starting and Stopping Trace Experiments](Starting-and-Stopping-Trace-Experiments.html#Starting-and-Stopping-Trace-Experiments)]
:::

---

#### 13.1.8 Listing Static Tracepoint Markers

`info static-tracepoint-markers`

Display information about all static tracepoint markers defined in the program.

For each marker, the following columns are printed:

*Count*

:   An incrementing counter, output to help readability. This is not a stable identifier.

*ID*

:   The marker ID, as reported by the target.

*Enabled or Disabled*

:   Probed markers are tagged with '`y`' identifies marks that are not enabled.

*Address*

:   Where the marker is in your program, as a memory address.

*What*

:   Where the marker is in the source for your program, as a file and line number. If the debug information included in the program does not allow [GDB] to locate the source of the marker, this column will be left blank.

In addition, the following information may be printed for each marker:

*Data*

:   User data passed to the tracing library by the marker call. In the UST backend, this is the format string passed as argument to the marker call.

*Static tracepoints probing the marker*

:   The list of static tracepoints attached to the marker.

::: smallexample

```bash
(gdb) info static-tracepoint-markers
Cnt ID         Enb Address            What
1   ust/bar2   y   0x0000000000400e1a in main at stexample.c:25
     Data: number1 %d number2 %d
     Probed by static tracepoints: #2
2   ust/bar33  n   0x0000000000400c87 in main at stexample.c:24
     Data: str %s
(gdb)
```

:::
