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

On some systems, you can set breakpoints in shared libraries before the executable is run.

A *watchpoint* is a special breakpoint that stops your program when the value of an expression changes. The expression may be a value of a variable, or it could involve values of one or more variables combined by operators, such as '`a + b`'. This is sometimes called *data breakpoints*. You must use a different command to set watchpoints (see [Setting Watchpoints](Set-Watchpoints.html#Set-Watchpoints)), but aside from that, you can manage a watchpoint like any other breakpoint: you enable, disable, and delete both breakpoints and watchpoints using the same commands.

You can arrange to have values from your program displayed automatically whenever [GDB] stops at a breakpoint. See [Automatic Display](Auto-Display.html#Auto-Display).

A *catchpoint* is another special breakpoint that stops your program when a certain kind of event occurs, such as the throwing of a C++ exception or the loading of a library. As with watchpoints, you use a different command to set a catchpoint (see [Setting Catchpoints](Set-Catchpoints.html#Set-Catchpoints)), but aside from that, you can manage a catchpoint like any other breakpoint. (To stop when your program receives a signal, use the `handle` command; see [Signals](Signals.html#Signals).)

[GDB] assigns a number to each breakpoint, watchpoint, or catchpoint when you create it; these numbers are successive integers starting with one. In many of the commands for controlling various features of breakpoints you use the breakpoint number to say which breakpoint you want to change. Each breakpoint may be *enabled* or *disabled*; if disabled, it has no effect on your program until you enable it again.

Some [GDB]'. When a breakpoint list is given to a command, all breakpoints in that list are operated on.

---

• [Set Breaks](Set-Breaks.html#Set-Breaks):                                                    Setting breakpoints
• [Set Watchpoints](Set-Watchpoints.html#Set-Watchpoints):                                     Setting watchpoints
• [Set Catchpoints](Set-Catchpoints.html#Set-Catchpoints):                                     Setting catchpoints
• [Delete Breaks](Delete-Breaks.html#Delete-Breaks):                                           Deleting breakpoints
• [Disabling](Disabling.html#Disabling):                                                       Disabling breakpoints
• [Conditions](Conditions.html#Conditions):                                                    Break conditions
• [Break Commands](Break-Commands.html#Break-Commands):                                        Breakpoint command lists
• [Dynamic Printf](Dynamic-Printf.html#Dynamic-Printf):                                        Dynamic printf
• [Save Breakpoints](Save-Breakpoints.html#Save-Breakpoints):                                  How to save breakpoints in a file
• [Static Probe Points](Static-Probe-Points.html#Static-Probe-Points):                                        Listing static probe points
• [Error in Breakpoints](Error-in-Breakpoints.html#Error-in-Breakpoints):                                     "Cannot insert breakpoints"
• [Breakpoint-related Warnings](Breakpoint_002drelated-Warnings.html#Breakpoint_002drelated-Warnings):        "Breakpoint address adjusted\..."

---

---

::: header
Next: [Continuing and Stepping](Continuing-and-Stepping.html#Continuing-and-Stepping)]
:::
