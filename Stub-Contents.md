---
tip: translate by openai@2023-06-23 13:41:07
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

> 这个例程安排了当您的程序停止时运行`handle_exception`。您必须在程序的启动代码中明确调用此子程序。

`handle_exception`


This is the central workhorse, but your program never calls it explicitly---the setup code arranges for `handle_exception` to run when a trap is triggered.

> 这是中央的工作马，但是你的程序从不会明确地调用它---设置代码会安排`handle_exception`在捕获触发时运行。

`handle_exception` takes control when your program stops during execution (for example, on a breakpoint), and mediates communications with [GDB] command that makes your program resume; at that point, `handle_exception` returns control to your own code on the target machine.

`breakpoint`


Use this auxiliary subroutine to make your program contain a breakpoint. Depending on the particular situation, this may be the only way for [GDB] session gets control.

> 使用这个辅助子程序来使你的程序包含一个断点。根据特定情况，这可能是[GDB]会话得到控制的唯一方式。


Call `breakpoint` if none of these is true, or if you simply want to make certain your program stops at a predetermined point for the start of your debugging session.

> 如果以上都不成立，或者只是想确保程序在调试会话开始时在预定点停止，请调用`断点`。

---

::: header
Next: [Bootstrapping](Bootstrapping.html#Bootstrapping)]
:::
