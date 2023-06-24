---
tip: translate by openai@2023-06-23 17:10:20
...
---
description: Altering (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Altering (Debugging with GDB)
lang: en
resource-type: document
title: Altering (Debugging with GDB)
---
::: header
Next: [GDB Files](GDB-Files.html#GDB-Files)]
:::

---

## 17 Altering Execution


Once you think you have found an error in your program, you might want to find out for certain whether correcting the apparent error would lead to correct results in the rest of the run. You can find the answer by experiment, using the [GDB] features for altering execution of the program.

> 一旦你认为在你的程序中发现了一个错误，你可能想要确定修正明显的错误是否会导致运行的其余部分的正确结果。您可以通过使用[GDB]功能来改变程序的执行来进行实验来找到答案。


For example, you can store new values into variables or memory locations, give your program a signal, restart it at a different address, or even return prematurely from a function.

> 例如，您可以将新值存储到变量或存储位置，向程序发出信号，在不同地址重新启动它，甚至可以从函数中提前返回。

---


• [Assignment](Assignment.html#Assignment):                                                              Assignment to variables

> • [任务](Assignment.html#Assignment):  将任务分配给变量

• [Jumping](Jumping.html#Jumping):                                                                       Continuing at a different address

> • [跳跃](Jumping.html#Jumping):                                                                       在不同的地址继续

• [Signaling](Signaling.html#Signaling):                                                                 Giving your program a signal

> • 信号传递（Signaling）：给你的程序发出信号

• [Returning](Returning.html#Returning):                                                                 Returning from a function

> • [返回](Returning.html#Returning)：从函数返回

• [Calling](Calling.html#Calling):                                                                       Calling your program's functions

> • [呼叫](Calling.html#Calling)：呼叫您的程序的功能。

• [Patching](Patching.html#Patching):                                                                    Patching your program

> •[补丁](Patching.html#Patching)：补丁你的程序

• [Compiling and Injecting Code](Compiling-and-Injecting-Code.html#Compiling-and-Injecting-Code)

> • [编译和注入代码](Compiling-and-Injecting-Code.html#Compiling-and-Injecting-Code)

---
