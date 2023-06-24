---
tip: translate by openai@2023-06-23 18:23:43
...
---
description: Breakpoints (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Breakpoints (Debugging with GDB)
lang: en
resource-type: document
title: Breakpoints (Debugging with GDB)
---
::: header
Next: [Continuing and Stepping](Continuing-and-Stepping.html#Continuing-and-Stepping)]
:::

---

### 5.1 Breakpoints, Watchpoints, and Catchpoints


A *breakpoint* makes your program stop whenever a certain point in the program is reached. For each breakpoint, you can add conditions to control in finer detail whether your program stops. You can set breakpoints with the `break` command and its variants (see [Setting Breakpoints](Set-Breaks.html#Set-Breaks)), to specify the place where your program should stop by line number, function name or exact address in the program.

> 断点可以让您的程序在程序到达某个特定点时停止。对于每个断点，您可以添加条件以更精细地控制程序是否停止。您可以使用`break`命令及其变体（参见[设置断点](Set-Breaks.html#Set-Breaks)）设置断点，以指定程序应该以行号、函数名或程序中的精确地址停止的位置。


On some systems, you can set breakpoints in shared libraries before the executable is run.

> 在某些系统中，在执行可执行文件之前，可以在共享库中设置断点。


A *watchpoint* is a special breakpoint that stops your program when the value of an expression changes. The expression may be a value of a variable, or it could involve values of one or more variables combined by operators, such as '`a + b`'. This is sometimes called *data breakpoints*. You must use a different command to set watchpoints (see [Setting Watchpoints](Set-Watchpoints.html#Set-Watchpoints)), but aside from that, you can manage a watchpoint like any other breakpoint: you enable, disable, and delete both breakpoints and watchpoints using the same commands.

> 一个*断点*是一个特殊的断点，当表达式的值发生变化时，它会停止程序的执行。表达式可以是变量的值，也可以是由一个或多个变量结合运算符（如'a + b'）组成的表达式。这有时也被称为*数据断点*。设置断点需要使用不同的命令（参见[设置断点](Set-Watchpoints.html#Set-Watchpoints)），但是除此之外，您可以像管理任何其他断点一样管理断点和断点：您可以使用相同的命令启用、禁用和删除断点和断点。


You can arrange to have values from your program displayed automatically whenever [GDB] stops at a breakpoint. See [Automatic Display](Auto-Display.html#Auto-Display).

> 您可以安排在GDB在断点处停止时自动显示程序中的值。请参阅“自动显示”(Auto-Display.html#Auto-Display)。


A *catchpoint* is another special breakpoint that stops your program when a certain kind of event occurs, such as the throwing of a C++ exception or the loading of a library. As with watchpoints, you use a different command to set a catchpoint (see [Setting Catchpoints](Set-Catchpoints.html#Set-Catchpoints)), but aside from that, you can manage a catchpoint like any other breakpoint. (To stop when your program receives a signal, use the `handle` command; see [Signals](Signals.html#Signals).)

> 一个*捕获点*是另一个特殊的断点，当某种特定的事件发生时，如抛出C++异常或加载库时，它会停止程序。与监视点一样，您使用不同的命令来设置捕获点（请参见[设置捕获点](Set-Catchpoints.html#Set-Catchpoints)），但除此之外，您可以像管理其他断点一样管理捕获点。 （要停止程序接收信号时，请使用`handle`命令；请参见[信号](Signals.html#Signals)。）


[GDB] assigns a number to each breakpoint, watchpoint, or catchpoint when you create it; these numbers are successive integers starting with one. In many of the commands for controlling various features of breakpoints you use the breakpoint number to say which breakpoint you want to change. Each breakpoint may be *enabled* or *disabled*; if disabled, it has no effect on your program until you enable it again.

> GDB在创建断点、监视点或捕获点时，会为每个断点分配一个编号；这些编号是从1开始的连续整数。在控制断点特性的许多命令中，您可以使用断点编号来指定要更改的断点。每个断点可以*启用*或*禁用*；如果禁用，则在您再次启用它之前，它不会对您的程序产生任何影响。


Some [GDB]'. When a breakpoint list is given to a command, all breakpoints in that list are operated on.

> 当给定一个断点列表时，GDB会对该列表中的所有断点进行操作。

---


• [Set Breaks](Set-Breaks.html#Set-Breaks):                                                    Setting breakpoints

> • [设置断点](Set-Breaks.html#Set-Breaks): 设置断点

• [Set Watchpoints](Set-Watchpoints.html#Set-Watchpoints):                                     Setting watchpoints

> • [设置观察点](Set-Watchpoints.html#Set-Watchpoints):                                     设置观察点

• [Set Catchpoints](Set-Catchpoints.html#Set-Catchpoints):                                     Setting catchpoints

> • [设置捕获点](Set-Catchpoints.html#Set-Catchpoints): 设置捕获点

• [Delete Breaks](Delete-Breaks.html#Delete-Breaks):                                           Deleting breakpoints

> • [删除断点](Delete-Breaks.html#Delete-Breaks): 删除断点

• [Disabling](Disabling.html#Disabling):                                                       Disabling breakpoints

> • [停用](Disabling.html#Disabling): 停用断点

• [Conditions](Conditions.html#Conditions):                                                    Break conditions

> • [条件](Conditions.html#Conditions):                                                打破条件

• [Break Commands](Break-Commands.html#Break-Commands):                                        Breakpoint command lists

> • [断点命令](Break-Commands.html#Break-Commands): 断点命令列表

• [Dynamic Printf](Dynamic-Printf.html#Dynamic-Printf):                                        Dynamic printf

> • [动态Printf](Dynamic-Printf.html#Dynamic-Printf):                                   动态printf

• [Save Breakpoints](Save-Breakpoints.html#Save-Breakpoints):                                  How to save breakpoints in a file

> • [保存断点](Save-Breakpoints.html#Save-Breakpoints):                                  如何将断点保存到文件中

• [Static Probe Points](Static-Probe-Points.html#Static-Probe-Points):                                        Listing static probe points

> • [静态探针点](Static-Probe-Points.html#Static-Probe-Points):                            列出静态探针点

• [Error in Breakpoints](Error-in-Breakpoints.html#Error-in-Breakpoints):                                     "Cannot insert breakpoints"

> • [错误断点](Error-in-Breakpoints.html#Error-in-Breakpoints): "无法插入断点"

• [Breakpoint-related Warnings](Breakpoint_002drelated-Warnings.html#Breakpoint_002drelated-Warnings):        "Breakpoint address adjusted\..."

> • [警告与断点有关](Breakpoint_002drelated-Warnings.html#Breakpoint_002drelated-Warnings):        "断点地址已调整\..."

---

---

::: header
Next: [Continuing and Stepping](Continuing-and-Stepping.html#Continuing-and-Stepping)]
:::
