---
tip: translate by openai@2023-06-23 17:50:37
...
---
description: Background Execution (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Background Execution (Debugging with GDB)
lang: en
resource-type: document
title: Background Execution (Debugging with GDB)
---
::: header
Next: [Thread-Specific Breakpoints](Thread_002dSpecific-Breakpoints.html#Thread_002dSpecific-Breakpoints)]
:::

---

#### 5.5.3 Background Execution


[GDB] immediately gives a command prompt so that you can issue other commands while your program runs.

> GDB 立即给出一个命令提示符，以便您在程序运行时发出其他命令。


If the target doesn't support async mode, [GDB] issues an error message if you attempt to use the background execution commands.

> 如果目标不支持异步模式，如果尝试使用后台执行命令，[GDB]将会发出错误消息。


To specify background execution, add a `&` to the command. For example, the background form of the `continue` command is `continue&`, or just `c&`. The execution commands that accept background execution are:

> 要指定后台执行，请在命令后面加上`&`。例如，`continue`命令的后台形式为`continue&`，或只需写`c&`。接受后台执行的执行命令有：

`run`


See [Starting your Program](Starting.html#Starting).

> 请参阅[启动程序](Starting.html#Starting)。

`attach`


See [Debugging an Already-running Process](Attach.html#Attach).

> 请参阅[调试正在运行的进程](Attach.html#Attach)。

`step`


See [step](Continuing-and-Stepping.html#Continuing-and-Stepping).

> 看[步骤](Continuing-and-Stepping.html#Continuing-and-Stepping)。

`stepi`


See [stepi](Continuing-and-Stepping.html#Continuing-and-Stepping).

> 看[stepi](Continuing-and-Stepping.html#Continuing-and-Stepping)。

`next`


See [next](Continuing-and-Stepping.html#Continuing-and-Stepping).

> 看[下一页](Continuing-and-Stepping.html#Continuing-and-Stepping)。

`nexti`


See [nexti](Continuing-and-Stepping.html#Continuing-and-Stepping).

> 见[下一步](Continuing-and-Stepping.html#Continuing-and-Stepping)。

`continue`


See [continue](Continuing-and-Stepping.html#Continuing-and-Stepping).

> 请参阅[继续](Continuing-and-Stepping.html#Continuing-and-Stepping)。

`finish`


See [finish](Continuing-and-Stepping.html#Continuing-and-Stepping).

> 看[完成](Continuing-and-Stepping.html#Continuing-and-Stepping)。

`until`


See [until](Continuing-and-Stepping.html#Continuing-and-Stepping).

> 请参见[直到](Continuing-and-Stepping.html#Continuing-and-Stepping)。


Background execution is especially useful in conjunction with non-stop mode for debugging programs with multiple threads; see [Non-Stop Mode](Non_002dStop-Mode.html#Non_002dStop-Mode). However, you can also use these commands in the normal all-stop mode with the restriction that you cannot issue another execution command until the previous one finishes. Examples of commands that are valid in all-stop mode while the program is running include `help` and `info break`.

> 背景执行特别有用，可以与非停止模式配合使用，用于调试具有多个线程的程序；参见[非停止模式](Non_002dStop-Mode.html#Non_002dStop-Mode)。但是，您也可以在正常的全停止模式下使用这些命令，但有一个限制，即您不能在上一个命令完成之前发出另一个执行命令。可以在程序运行时在全停止模式下使用的命令示例包括`帮助`和`信息断点`。


You can interrupt your program while it is running in the background by using the `interrupt` command.

> 你可以在程序在后台运行时使用`interrupt`命令中断它。

`interrupt`

`interrupt -a`


Suspend execution of the running program. In all-stop mode, `interrupt` stops the whole process, but in non-stop mode, it stops only the current thread. To stop the whole program in non-stop mode, use `interrupt -a`.

> 暂停正在运行的程序的执行。在全停止模式下，`中断`会停止整个进程，但是在非停止模式下，只会停止当前线程。要在非停止模式下停止整个程序，请使用`中断-a`。

---

::: header
Next: [Thread-Specific Breakpoints](Thread_002dSpecific-Breakpoints.html#Thread_002dSpecific-Breakpoints)]
:::
