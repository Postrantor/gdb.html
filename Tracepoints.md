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

Using [GDB] records these values without interacting with you, it can do so quickly and unobtrusively, hopefully not disturbing the program's behavior.

The tracepoint facility is currently available only for remote targets. See [Targets](Targets.html#Targets). In addition, your remote target must know how to collect trace data. This functionality is implemented in the remote stub; however, none of the stubs distributed with [GDB] support tracepoints as of this writing. The format of the remote packets used to implement tracepoints are described in [Tracepoint Packets](Tracepoint-Packets.html#Tracepoint-Packets).

It is also possible to get trace data from a file, in a manner reminiscent of corefiles; you specify the filename, and use `tfind` to search through the file. See [Trace Files](Trace-Files.html#Trace-Files), for more details.

This chapter describes the tracepoint commands and features.

---

• [Set Tracepoints](Set-Tracepoints.html#Set-Tracepoints):                          
• [Analyze Collected Data](Analyze-Collected-Data.html#Analyze-Collected-Data):     
• [Tracepoint Variables](Tracepoint-Variables.html#Tracepoint-Variables):           
• [Trace Files](Trace-Files.html#Trace-Files):                                      

---

---

::: header
Next: [Overlays](Overlays.html#Overlays)]
:::
