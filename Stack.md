---
tip: translate by openai@2023-06-24 03:07:13
...
---
description: Stack (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Stack (Debugging with GDB)
lang: en
resource-type: document
title: Stack (Debugging with GDB)
---
::: header
Next: [Source](Source.html#Source)]
:::

---

## 8 Examining the Stack


When your program has stopped, the first thing you need to know is where it stopped and how it got there.

> 当你的程序停止运行时，你首先需要知道它停在哪里以及是怎样到达那里的。


Each time your program performs a function call, information about the call is generated. That information includes the location of the call in your program, the arguments of the call, and the local variables of the function being called. The information is saved in a block of data called a *stack frame*. The stack frames are allocated in a region of memory called the *call stack*.

> 每次您的程序执行函数调用时，就会生成有关调用的信息。该信息包括程序中调用的位置、调用的参数以及被调用函数的局部变量。该信息保存在一个名为*堆栈帧*的数据块中。堆栈帧分配在一个叫做*调用堆栈*的内存区域中。


When your program stops, the [GDB] commands for examining the stack allow you to see all of this information.

> 当您的程序停止时，[GDB]检查堆栈的命令可以让您查看所有这些信息。


One of the stack frames is *selected* by [GDB] commands to select whichever frame you are interested in. See [Selecting a Frame](Selection.html#Selection).

> 一个堆栈帧可以通过GDB命令选择你感兴趣的帧。请参阅[选择帧](Selection.html#Selection)。


When your program stops, [GDB] automatically selects the currently executing frame and describes it briefly, similar to the `frame` command (see [Information about a Frame](Frame-Info.html#Frame-Info)).

> 当您的程序停止时，[GDB]会自动选择当前正在执行的帧，并简要描述它，类似于`frame`命令（参见[关于帧的信息](Frame-Info.html#Frame-Info)）。

+:--------------------------------------------------------------------------------------------------+-----------------------+:-------------------------------------+
| • [Frames](Frames.html#Frames):                                                    |                       | Stack frames                         |
+---------------------------------------------------------------------------------------------------+-----------------------+--------------------------------------+
| • [Backtrace](Backtrace.html#Backtrace):                                           |                       | Backtraces                           |
+---------------------------------------------------------------------------------------------------+-----------------------+--------------------------------------+
| • [Selection](Selection.html#Selection):                                           |                       | Selecting a frame                    |
+---------------------------------------------------------------------------------------------------+-----------------------+--------------------------------------+
| • [Frame Info](Frame-Info.html#Frame-Info):                                        |                       | Information on a frame               |
+---------------------------------------------------------------------------------------------------+-----------------------+--------------------------------------+
| • [Frame Apply](Frame-Apply.html#Frame-Apply):                                     |                       | Applying a command to several frames |
+---------------------------------------------------------------------------------------------------+-----------------------+--------------------------------------+
| • [Frame Filter Management](Frame-Filter-Management.html#Frame-Filter-Management): |                       | Managing frame filters               |
+---------------------------------------------------------------------------------------------------+-----------------------+--------------------------------------+
| ``menu-comment                                                                                  |                       |                                      | |``                                                                                               |                       |                                      |
+---------------------------------------------------------------------------------------------------+-----------------------+--------------------------------------+

---

::: header
Next: [Source](Source.html#Source)]
:::
