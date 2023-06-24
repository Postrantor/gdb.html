---
tip: translate by openai@2023-06-23 20:30:39
...
---
description: Delete Breaks (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Delete Breaks (Debugging with GDB)
lang: en
resource-type: document
title: Delete Breaks (Debugging with GDB)
---
::: header
Next: [Disabling](Disabling.html#Disabling)]
:::

---

#### 5.1.4 Deleting Breakpoints


It is often necessary to eliminate a breakpoint, watchpoint, or catchpoint once it has done its job and you no longer want your program to stop there. This is called *deleting* the breakpoint. A breakpoint that has been deleted no longer exists; it is forgotten.

> 常常有必要删除断点、监视点或捕获点，一旦它完成了它的工作，你不再希望程序在那里停止。这就叫做*删除*断点。已经被删除的断点不再存在；它被遗忘了。


With the `clear` command you can delete breakpoints according to where they are in your program. With the `delete` command you can delete individual breakpoints, watchpoints, or catchpoints by specifying their breakpoint numbers.

> 使用`clear`命令，您可以根据程序中的位置删除断点。使用`delete`命令，您可以通过指定断点号来删除单个断点、监视点或捕获点。


It is not necessary to delete a breakpoint to proceed past it. [GDB] automatically ignores breakpoints on the first instruction to be executed when you continue execution without changing the execution address.

> 不需要删除断点才能继续执行。[GDB] 在您继续执行而不更改执行地址的情况下，会自动忽略第一条要执行的指令上的断点。

`clear`


Delete any breakpoints at the next instruction to be executed in the selected stack frame (see [Selecting a Frame](Selection.html#Selection)). When the innermost frame is selected, this is a good way to delete a breakpoint where your program just stopped.

> 删除选定堆栈帧中要执行的下一条指令的任何断点（参见[选择帧]（Selection.html#Selection））。当选择最内层帧时，这是删除程序刚停止的断点的好方法。

`clear locspec`

Delete any breakpoint with a code location that corresponds to `locspec`:

`linenum`
`filename:linenum`
`-line linenum`
`-source filename -line linenum`

:   If `locspec` is omitted, it defaults to the current source file.

`*address`

:   If `locspec`.

`function`
`-function function`

:   If `locspec`.


Ambiguity in names of files and functions can be resolved as described in [Location Specifications](Location-Specifications.html#Location-Specifications).

> 文件和函数名称的模糊性可以按照[位置规范](Location-Specifications.html#Location-Specifications)中的描述来解决。

`delete [breakpoints] [list…]`


Delete the breakpoints, watchpoints, or catchpoints of the breakpoint list specified as argument. If no argument is specified, delete all breakpoints ([GDB] asks confirmation, unless you have `set confirm off`). You can abbreviate this command as `d`.

> 从指定的断点列表中删除断点、监视点或捕捉点。如果未指定参数，则删除所有断点（[GDB]会询问确认，除非您已经关闭了`set confirm off`）。您可以将此命令简写为`d`。

---

::: header
Next: [Disabling](Disabling.html#Disabling)]
:::
