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

If the target doesn't support async mode, [GDB] issues an error message if you attempt to use the background execution commands.

To specify background execution, add a `&` to the command. For example, the background form of the `continue` command is `continue&`, or just `c&`. The execution commands that accept background execution are:

`run`

See [Starting your Program](Starting.html#Starting).

`attach`

See [Debugging an Already-running Process](Attach.html#Attach).

`step`

See [step](Continuing-and-Stepping.html#Continuing-and-Stepping).

`stepi`

See [stepi](Continuing-and-Stepping.html#Continuing-and-Stepping).

`next`

See [next](Continuing-and-Stepping.html#Continuing-and-Stepping).

`nexti`

See [nexti](Continuing-and-Stepping.html#Continuing-and-Stepping).

`continue`

See [continue](Continuing-and-Stepping.html#Continuing-and-Stepping).

`finish`

See [finish](Continuing-and-Stepping.html#Continuing-and-Stepping).

`until`

See [until](Continuing-and-Stepping.html#Continuing-and-Stepping).

Background execution is especially useful in conjunction with non-stop mode for debugging programs with multiple threads; see [Non-Stop Mode](Non_002dStop-Mode.html#Non_002dStop-Mode). However, you can also use these commands in the normal all-stop mode with the restriction that you cannot issue another execution command until the previous one finishes. Examples of commands that are valid in all-stop mode while the program is running include `help` and `info break`.

You can interrupt your program while it is running in the background by using the `interrupt` command.

`interrupt`

`interrupt -a`

Suspend execution of the running program. In all-stop mode, `interrupt` stops the whole process, but in non-stop mode, it stops only the current thread. To stop the whole program in non-stop mode, use `interrupt -a`.

---

::: header
Next: [Thread-Specific Breakpoints](Thread_002dSpecific-Breakpoints.html#Thread_002dSpecific-Breakpoints)]
:::
