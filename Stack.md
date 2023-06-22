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

Each time your program performs a function call, information about the call is generated. That information includes the location of the call in your program, the arguments of the call, and the local variables of the function being called. The information is saved in a block of data called a *stack frame*. The stack frames are allocated in a region of memory called the *call stack*.

When your program stops, the [GDB] commands for examining the stack allow you to see all of this information.

One of the stack frames is *selected* by [GDB] commands to select whichever frame you are interested in. See [Selecting a Frame](Selection.html#Selection).

When your program stops, [GDB] automatically selects the currently executing frame and describes it briefly, similar to the `frame` command (see [Information about a Frame](Frame-Info.html#Frame-Info)).

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
