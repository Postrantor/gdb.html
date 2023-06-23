---
description: Stopping (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Stopping (Debugging with GDB)
lang: en
resource-type: document
title: Stopping (Debugging with GDB)
---
::: header
Next: [Reverse Execution](Reverse-Execution.html#Reverse-Execution)]
:::

---

## 5 Stopping and Continuing

The principal purposes of using a debugger are so that you can stop your program before it terminates; or so that, if your program runs into trouble, you can investigate and find out why.

Inside [GDB] provide ample explanation of the status of your program---but you can also explicitly request this information at any time.

`info program`

Display information about the status of your program: whether it is running or not, what process it is, and why it stopped.

---

• [Breakpoints](Breakpoints.html#Breakpoints):                                                                          Breakpoints, watchpoints, and catchpoints
• [Continuing and Stepping](Continuing-and-Stepping.html#Continuing-and-Stepping):                                      Resuming execution
• [Skipping Over Functions and Files](Skipping-Over-Functions-and-Files.html#Skipping-Over-Functions-and-Files):        Skipping over functions and files
• [Signals](Signals.html#Signals):                                                                                      Signals
• [Thread Stops](Thread-Stops.html#Thread-Stops):                                                                       Stopping and starting multi-thread programs

---
