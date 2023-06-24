---
tip: translate by openai@2023-06-23 20:32:30
...
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

> 代替刪除斷點、監視點或捕捉點，你可能更喜歡*禁用*它們。這使斷點失效，就像已經被刪除一樣，但記住斷點的信息，以便你可以*啟用*它以後再次使用。


You disable and enable breakpoints, watchpoints, and catchpoints with the `enable` and `disable` commands, optionally specifying one or more breakpoint numbers as arguments. Use `info break` to print a list of all breakpoints, watchpoints, and catchpoints if you do not know which numbers to use.

> 你可以使用`enable`和`disable`命令来启用和禁用断点、监视点和捕获点，可以可选择性地指定一个或多个断点编号作为参数。如果你不知道要使用哪些编号，可以使用`info break`来打印所有断点、监视点和捕获点的列表。


Disabling and enabling a breakpoint that has multiple locations affects all of its locations.

> 禁用和启用具有多个位置的断点会影响它的所有位置。


A breakpoint, watchpoint, or catchpoint can have any of several different states of enablement:

> 断点、监视点或捕获点可以具有多种不同的使能状态：


- Enabled. The breakpoint stops your program. A breakpoint set with the `break` command starts out in this state.

> 启用。断点会停止您的程序。使用 `break` 命令设置的断点最初处于此状态。
- Disabled. The breakpoint has no effect on your program.
- Enabled once. The breakpoint stops your program, but then becomes disabled.

- Enabled for a count. The breakpoint stops your program for the next N times, then becomes disabled.

> 已启用计数。断点会在接下来的N次后停止您的程序，然后会失效。

- Enabled for deletion. The breakpoint stops your program, but immediately after it does so it is deleted permanently. A breakpoint set with the `tbreak` command starts out in this state.

> 已启用删除。断点会停止您的程序，但在此之后，它将永久删除。使用`tbreak`命令设置的断点最初处于此状态。


You can use the following commands to enable or disable breakpoints, watchpoints, and catchpoints:

> 您可以使用以下命令启用或禁用断点、监视点和捕获点：

`disable [breakpoints] [list…]`


Disable the specified breakpoints---or all breakpoints, if none are listed. A disabled breakpoint has no effect but is not forgotten. All options such as ignore-counts, conditions and commands are remembered in case the breakpoint is enabled again later. You may abbreviate `disable` as `dis`.

> 禁用指定断点---或者如果没有列出，则禁用所有断点。禁用断点不会产生任何效果，但不会被遗忘。所有选项，如忽略计数、条件和命令，都会被记住，以便稍后可以重新启用断点。您可以将“禁用”简写为“dis”。

`enable [breakpoints] [list…]`


Enable the specified breakpoints (or all defined breakpoints). They become effective once again in stopping your program.

> 启用指定的断点（或所有已定义的断点）。一旦再次停止程序，它们就会生效。

`enable [breakpoints] once list…`


Enable the specified breakpoints temporarily. [GDB] disables any of these breakpoints immediately after stopping your program.

> 启用指定的断点暂时。[GDB] 在停止程序后立即禁用其中任何断点。

`enable [breakpoints] count count list…`

Enable the specified breakpoints temporarily. [GDB] is affected.

`enable [breakpoints] delete list…`


Enable the specified breakpoints to work once, then die. [GDB] deletes any of these breakpoints as soon as your program stops there. Breakpoints set by the `tbreak` command start out in this state.

> 启用指定的断点，只工作一次，然后死亡。 [GDB] 一旦你的程序停在那里，就会删除这些断点中的任何一个。 由`tbreak`命令设置的断点最初处于此状态。


Except for a breakpoint set with `tbreak` (see [Setting Breakpoints](Set-Breaks.html#Set-Breaks)), breakpoints that you set are initially enabled; subsequently, they become disabled or enabled only when you use one of the commands above. (The command `until` can set and delete a breakpoint of its own, but it does not change the state of your other breakpoints; see [Continuing and Stepping](Continuing-and-Stepping.html#Continuing-and-Stepping).)

> 除了使用 `tbreak` 设置的断点（参见[设置断点](Set-Breaks.html#Set-Breaks)）外，您设置的断点最初都是启用的；之后，它们只有在使用上述命令时才会被禁用或启用。（命令`until`可以设置和删除自己的断点，但不会改变您的其他断点的状态；参见[继续和步进](Continuing-and-Stepping.html#Continuing-and-Stepping)）。

---

::: header
Next: [Conditions](Conditions.html#Conditions)]
:::
