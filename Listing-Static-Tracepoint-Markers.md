---
tip: translate by openai@2023-06-23 23:54:27
...
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

> 顯示有關程式中定義的所有靜態跟蹤點標記的資訊。

For each marker, the following columns are printed:

*Count*


:   An incrementing counter, output to help readability. This is not a stable identifier.

> 一个递增计数器，输出以提高可读性。这不是一个稳定的标识符。

*ID*

:   The marker ID, as reported by the target.

*Enabled or Disabled*


:   Probed markers are tagged with '`y`' identifies marks that are not enabled.

> 被探测的标记被标记为'y'，表示这些标记未被启用。

*Address*

:   Where the marker is in your program, as a memory address.

*What*


:   Where the marker is in the source for your program, as a file and line number. If the debug information included in the program does not allow [GDB] to locate the source of the marker, this column will be left blank.

> 在你的程序源文件中标记的位置是什么？用文件名和行号来表示。如果程序中包含的调试信息不能让GDB定位标记的源，那么这一列将留空。

In addition, the following information may be printed for each marker:

*Data*


:   User data passed to the tracing library by the marker call. In the UST backend, this is the format string passed as argument to the marker call.

> 用户数据通过标记调用传递给跟踪库。在UST后端，这是作为参数传递给标记调用的格式字符串。

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
