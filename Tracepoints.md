---
tip: translate by openai@2023-06-23 14:49:05
...
---
description: Tracepoints (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Tracepoints (Debugging with GDB)
lang: en
resource-type: document
title: Tracepoints (Debugging with GDB)
---
::: header
Next: [Overlays](Overlays.html#Overlays)]
:::

---

## 13 Tracepoints


In some applications, it is not feasible for the debugger to interrupt the program's execution long enough for the developer to learn anything helpful about its behavior. If the program's correctness depends on its real-time behavior, delays introduced by a debugger might cause the program to change its behavior drastically, or perhaps fail, even when the code itself is correct. It is useful to be able to observe the program's behavior without interrupting it.

> 在某些应用中，调试器无法中断程序执行足够长的时间，以便开发人员能够学习它的行为。如果程序的正确性取决于它的实时行为，调试器引入的延迟可能会导致程序的行为发生巨大变化，或者即使代码本身是正确的，也可能会失败。能够观察程序的行为而不中断它是有用的。


Using [GDB] records these values without interacting with you, it can do so quickly and unobtrusively, hopefully not disturbing the program's behavior.

> 使用GDB记录这些值而不与您交互，它可以快速而不显眼地完成，希望不会干扰程序的行为。


The tracepoint facility is currently available only for remote targets. See [Targets](Targets.html#Targets). In addition, your remote target must know how to collect trace data. This functionality is implemented in the remote stub; however, none of the stubs distributed with [GDB] support tracepoints as of this writing. The format of the remote packets used to implement tracepoints are described in [Tracepoint Packets](Tracepoint-Packets.html#Tracepoint-Packets).

> 目前，跟踪点功能仅适用于远程目标。请参见[目标]（Targets.html＃Targets）。此外，您的远程目标必须知道如何收集跟踪数据。此功能由远程存根实现；但是，在本文撰写之时，与[GDB]一起分发的存根都不支持跟踪点。用于实现跟踪点的远程数据包的格式在[跟踪点数据包]（Tracepoint-Packets.html＃Tracepoint-Packets）中描述。


It is also possible to get trace data from a file, in a manner reminiscent of corefiles; you specify the filename, and use `tfind` to search through the file. See [Trace Files](Trace-Files.html#Trace-Files), for more details.

> 也可以从文件中获取跟踪数据，这种方式类似于核心文件；您指定文件名，并使用`tfind`搜索文件。有关详细信息，请参阅[跟踪文件](Trace-Files.html#Trace-Files)。


This chapter describes the tracepoint commands and features.

> 本章节描述了跟踪点命令和功能。

---


• [Set Tracepoints](Set-Tracepoints.html#Set-Tracepoints):                          

> • [设置跟踪点](Set-Tracepoints.html#Set-Tracepoints):

• [Analyze Collected Data](Analyze-Collected-Data.html#Analyze-Collected-Data):     

> • [分析收集的数据](Analyze-Collected-Data.html#Analyze-Collected-Data):

• [Tracepoint Variables](Tracepoint-Variables.html#Tracepoint-Variables):           

> • [跟踪点变量](Tracepoint-Variables.html#Tracepoint-Variables):

• [Trace Files](Trace-Files.html#Trace-Files):                                      

> • [跟踪文件](Trace-Files.html#Trace-Files):

---

---

::: header
Next: [Overlays](Overlays.html#Overlays)]
:::
