---
tip: translate by openai@2023-06-23 17:16:11
...
---
description: Analyze Collected Data (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Analyze Collected Data (Debugging with GDB)
lang: en
resource-type: document
title: Analyze Collected Data (Debugging with GDB)
---
::: header
Next: [Tracepoint Variables](Tracepoint-Variables.html#Tracepoint-Variables)]
:::

---

### 13.2 Using the Collected Data


After the tracepoint experiment ends, you use [GDB] commands (`print`, `info registers`, `backtrace`, etc.) will behave as if we were currently debugging the program state as it was when the tracepoint occurred. Any requests for data that are not in the buffer will fail.

> 在跟踪点实验结束后，使用[GDB]命令（`print`，`info registers`，`backtrace`等）将就像我们正在调试跟踪点发生时程序的状态一样。任何不在缓冲区中的数据请求将会失败。

---


• [tfind](tfind.html#tfind):                                         How to select a trace snapshot

> • [tfind](tfind.html#tfind): 如何选择跟踪快照

• [tdump](tdump.html#tdump):                                         How to display all data for a snapshot

> • [tdump](tdump.html#tdump): 如何显示快照的所有数据

• [save tracepoints](save-tracepoints.html#save-tracepoints):        How to save tracepoints for a future run

> • [保存断点](save-tracepoints.html#save-tracepoints):  如何保存断点以备将来使用

---
