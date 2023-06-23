---
description: Disabling (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Disabling (Debugging with GDB)
lang: en
resource-type: document
title: Disabling (Debugging with GDB)
---
::: header
Next: [Conditions](Conditions.html#Conditions)]
:::

---

#### 5.1.5 Disabling Breakpoints

Rather than deleting a breakpoint, watchpoint, or catchpoint, you might prefer to *disable* it. This makes the breakpoint inoperative as if it had been deleted, but remembers the information on the breakpoint so that you can *enable* it again later.

You disable and enable breakpoints, watchpoints, and catchpoints with the `enable` and `disable` commands, optionally specifying one or more breakpoint numbers as arguments. Use `info break` to print a list of all breakpoints, watchpoints, and catchpoints if you do not know which numbers to use.

Disabling and enabling a breakpoint that has multiple locations affects all of its locations.

A breakpoint, watchpoint, or catchpoint can have any of several different states of enablement:

- Enabled. The breakpoint stops your program. A breakpoint set with the `break` command starts out in this state.
- Disabled. The breakpoint has no effect on your program.
- Enabled once. The breakpoint stops your program, but then becomes disabled.
- Enabled for a count. The breakpoint stops your program for the next N times, then becomes disabled.
- Enabled for deletion. The breakpoint stops your program, but immediately after it does so it is deleted permanently. A breakpoint set with the `tbreak` command starts out in this state.

You can use the following commands to enable or disable breakpoints, watchpoints, and catchpoints:

`disable [breakpoints] [list…]`

Disable the specified breakpoints---or all breakpoints, if none are listed. A disabled breakpoint has no effect but is not forgotten. All options such as ignore-counts, conditions and commands are remembered in case the breakpoint is enabled again later. You may abbreviate `disable` as `dis`.

`enable [breakpoints] [list…]`

Enable the specified breakpoints (or all defined breakpoints). They become effective once again in stopping your program.

`enable [breakpoints] once list…`

Enable the specified breakpoints temporarily. [GDB] disables any of these breakpoints immediately after stopping your program.

`enable [breakpoints] count count list…`

Enable the specified breakpoints temporarily. [GDB] is affected.

`enable [breakpoints] delete list…`

Enable the specified breakpoints to work once, then die. [GDB] deletes any of these breakpoints as soon as your program stops there. Breakpoints set by the `tbreak` command start out in this state.

Except for a breakpoint set with `tbreak` (see [Setting Breakpoints](Set-Breaks.html#Set-Breaks)), breakpoints that you set are initially enabled; subsequently, they become disabled or enabled only when you use one of the commands above. (The command `until` can set and delete a breakpoint of its own, but it does not change the state of your other breakpoints; see [Continuing and Stepping](Continuing-and-Stepping.html#Continuing-and-Stepping).)

---

::: header
Next: [Conditions](Conditions.html#Conditions)]
:::
