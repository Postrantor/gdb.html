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

`set_debug_traps`

This routine arranges for `handle_exception` to run when your program stops. You must call this subroutine explicitly in your program's startup code.

`handle_exception`

This is the central workhorse, but your program never calls it explicitly---the setup code arranges for `handle_exception` to run when a trap is triggered.

`handle_exception` takes control when your program stops during execution (for example, on a breakpoint), and mediates communications with [GDB] command that makes your program resume; at that point, `handle_exception` returns control to your own code on the target machine.

`breakpoint`

Use this auxiliary subroutine to make your program contain a breakpoint. Depending on the particular situation, this may be the only way for [GDB] session gets control.

Call `breakpoint` if none of these is true, or if you simply want to make certain your program stops at a predetermined point for the start of your debugging session.

---

::: header
Next: [Bootstrapping](Bootstrapping.html#Bootstrapping)]
:::
