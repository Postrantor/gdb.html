---
tip: translate by openai@2023-06-23 14:29:26
...
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

> GDB也支持*非停止模式*，在该模式下，您可以在调试器中检查停止的线程时，其他线程可以继续自由运行。

---


• [All-Stop Mode](All_002dStop-Mode.html#All_002dStop-Mode):                                                  All threads stop when GDB takes control

> • [全停止模式](All_002dStop-Mode.html#All_002dStop-Mode): 当GDB控制时，所有线程都会停止。

• [Non-Stop Mode](Non_002dStop-Mode.html#Non_002dStop-Mode):                                                  Other threads continue to execute

> • [无停止模式](Non_002dStop-Mode.html#Non_002dStop-Mode): 其他线程继续执行

• [Background Execution](Background-Execution.html#Background-Execution):                                     Running your program asynchronously

> • [后台执行](Background-Execution.html#Background-Execution): 以异步方式运行您的程序

• [Thread-Specific Breakpoints](Thread_002dSpecific-Breakpoints.html#Thread_002dSpecific-Breakpoints):        Controlling breakpoints

> • [特定线程断点](Thread_002dSpecific-Breakpoints.html#Thread_002dSpecific-Breakpoints):        控制断点

• [Interrupted System Calls](Interrupted-System-Calls.html#Interrupted-System-Calls):                         GDB may interfere with system calls

> • [中断的系统调用](Interrupted-System-Calls.html#Interrupted-System-Calls): GDB 可能会干扰系统调用

• [Observer Mode](Observer-Mode.html#Observer-Mode):                                                          GDB does not alter program behavior

> • [观察者模式](Observer-Mode.html#Observer-Mode): GDB不会改变程序的行为。

---
