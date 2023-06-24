---
tip: translate by openai@2023-06-24 03:24:06
...
---
description: Stub Contents (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Stub Contents (Debugging with GDB)
lang: en
resource-type: document
title: Stub Contents (Debugging with GDB)
---
::: header
Next: [Bootstrapping](Bootstrapping.html#Bootstrapping)]
:::

---

#### 20.5.1 What the Stub Can Do for You


The debugging stub for your architecture supplies these three subroutines:

> 您的架构的调试存根提供了这三个子程序：

`set_debug_traps`


This routine arranges for `handle_exception` to run when your program stops. You must call this subroutine explicitly in your program's startup code.

> 此例程安排`handle_exception`在您的程序停止时运行。您必须在程序的启动代码中明确调用此子程序。

`handle_exception`


This is the central workhorse, but your program never calls it explicitly---the setup code arranges for `handle_exception` to run when a trap is triggered.

> 这是中央的主力，但您的程序从不显式地调用它---设置代码会安排`handle_exception`在触发陷阱时运行。

`handle_exception` takes control when your program stops during execution (for example, on a breakpoint), and mediates communications with [GDB] command that makes your program resume; at that point, `handle_exception` returns control to your own code on the target machine.

`breakpoint`


Use this auxiliary subroutine to make your program contain a breakpoint. Depending on the particular situation, this may be the only way for [GDB] session gets control.

> 使用此輔助子程序使您的程序包含斷點。根據特定情況，這可能是[GDB]會話獲得控制的唯一方法。


Call `breakpoint` if none of these is true, or if you simply want to make certain your program stops at a predetermined point for the start of your debugging session.

> 如果以上都不正确，或者您只是想让程序在预定的点停止以便开始调试会话，请调用`断点`。

---

::: header
Next: [Bootstrapping](Bootstrapping.html#Bootstrapping)]
:::
