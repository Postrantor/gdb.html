---
tip: translate by openai@2023-06-23 13:39:19
...
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

> 主要使用调试器的目的是让你在程序终止之前停止程序；或者如果程序出现问题，你可以调查并查明原因。


Inside [GDB] provide ample explanation of the status of your program---but you can also explicitly request this information at any time.

> 在GDB中，可以充分解释程序的状态，但您也可以随时明确要求此信息。

`info program`


Display information about the status of your program: whether it is running or not, what process it is, and why it stopped.

> 显示有关您程序状态的信息：它是否正在运行，是什么进程，以及为什么停止。

---


• [Breakpoints](Breakpoints.html#Breakpoints):                                                                          Breakpoints, watchpoints, and catchpoints

> • [断点](Breakpoints.html#Breakpoints)：断点、监视点和捕获点

• [Continuing and Stepping](Continuing-and-Stepping.html#Continuing-and-Stepping):                                      Resuming execution

> • [继续和跨步](Continuing-and-Stepping.html#Continuing-and-Stepping):                                      恢复执行

• [Skipping Over Functions and Files](Skipping-Over-Functions-and-Files.html#Skipping-Over-Functions-and-Files):        Skipping over functions and files

> • [跳过函数和文件](Skipping-Over-Functions-and-Files.html#Skipping-Over-Functions-and-Files):        跳过函数和文件

• [Signals](Signals.html#Signals):                                                                                      Signals

> •[信号](Signals.html#Signals)：信号

• [Thread Stops](Thread-Stops.html#Thread-Stops):                                                                       Stopping and starting multi-thread programs

> • [线程停止](Thread-Stops.html#Thread-Stops): 停止和启动多线程程序

---
