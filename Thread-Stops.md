---
description: Thread Stops (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Thread Stops (Debugging with GDB)
lang: en
resource-type: document
title: Thread Stops (Debugging with GDB)
---
::: header
Previous: [Signals](Signals.html#Signals)]
:::

---

### 5.5 Stopping and Starting Multi-thread Programs

[GDB] also supports *non-stop mode*, in which other threads can continue to run freely while you examine the stopped thread in the debugger.

---

• [All-Stop Mode](All_002dStop-Mode.html#All_002dStop-Mode):                                                  All threads stop when GDB takes control
• [Non-Stop Mode](Non_002dStop-Mode.html#Non_002dStop-Mode):                                                  Other threads continue to execute
• [Background Execution](Background-Execution.html#Background-Execution):                                     Running your program asynchronously
• [Thread-Specific Breakpoints](Thread_002dSpecific-Breakpoints.html#Thread_002dSpecific-Breakpoints):        Controlling breakpoints
• [Interrupted System Calls](Interrupted-System-Calls.html#Interrupted-System-Calls):                         GDB may interfere with system calls
• [Observer Mode](Observer-Mode.html#Observer-Mode):                                                          GDB does not alter program behavior

---
