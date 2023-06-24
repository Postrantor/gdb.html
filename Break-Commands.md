---
tip: translate by openai@2023-06-23 18:09:35
...
---
description: Break Commands (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Break Commands (Debugging with GDB)
lang: en
resource-type: document
title: Break Commands (Debugging with GDB)
---
::: header
Next: [Dynamic Printf](Dynamic-Printf.html#Dynamic-Printf)]
:::

---

#### 5.1.7 Breakpoint Command Lists


You can give any breakpoint (or watchpoint or catchpoint) a series of commands to execute when your program stops due to that breakpoint. For example, you might want to print the values of certain expressions, or enable other breakpoints.

> 你可以给任何断点（或监视点或捕获点）一系列命令，当你的程序由于该断点而停止时执行。例如，你可能想要打印某些表达式的值，或启用其他断点。

`commands [list…]`

`… command-list …`

`end`


Specify a list of commands for the given breakpoints. The commands themselves appear on the following lines. Type a line containing just `end` to terminate the commands.

> 指定给定断点的命令列表。命令本身出现在下面几行中。输入一行只包含`end`的行以终止命令。


To remove all commands from a breakpoint, type `commands` and follow it immediately with `end`; that is, give no commands.

> 要从断点中删除所有命令，请键入`commands`，然后立即跟上`end`；也就是说，不要给出任何命令。


With no argument, `commands` refers to the last breakpoint, watchpoint, or catchpoint set (not to the breakpoint most recently encountered). If the most recent breakpoints were set with a single command, then the `commands` will apply to all the breakpoints set by that command. This applies to breakpoints set by `rbreak`, and also applies when a single `break` command creates multiple breakpoints (see [Ambiguous Expressions](Ambiguous-Expressions.html#Ambiguous-Expressions)).

> 没有参数时，`commands`指的是最后一个断点、监视点或捕获点（而不是最近遇到的断点）。如果最近的断点是用一条命令设置的，那么`commands`将适用于该命令设置的所有断点。这适用于使用`rbreak`设置的断点，也适用于单个`break`命令创建多个断点的情况（参见[Ambiguous Expressions](Ambiguous-Expressions.html#Ambiguous-Expressions)）。


Pressing RET as a means of repeating the last [GDB].

> 按下RET作为重复上一个[GDB]的手段。


Inside a command list, you can use the command [disable \$_hit_bpnum] to disable the encountered breakpoint.

> 在命令列表中，您可以使用命令[disable \$_hit_bpnum]来禁用遇到的断点。


If your breakpoint has several code locations, the command [disable \$_hit_bpnum.\$_hit_locno] will disable the specific breakpoint code location encountered. If the breakpoint has only one location, this command will disable the encountered breakpoint.

> 如果您的断点有多个代码位置，则命令[disable \$_hit_bpnum.\$_hit_locno]将禁用遇到的特定断点代码位置。如果断点只有一个位置，则此命令将禁用遇到的断点。


You can use breakpoint commands to start your program up again. Simply use the `continue` command, or `step`, or any other command that resumes execution.

> 你可以使用断点命令来重新启动你的程序。只需使用`continue`命令，或者`step`命令，或者其他任何恢复执行的命令即可。


Any other commands in the command list, after a command that resumes execution, are ignored. This is because any time you resume execution (even with a simple `next` or `step`), you may encounter another breakpoint---which could have its own command list, leading to ambiguities about which list to execute.

> 在一个执行恢复的命令后面的命令列表中的任何其他命令都会被忽略。这是因为每当你恢复执行（甚至只是一个简单的“next”或“step”），你可能会遇到另一个断点---它可能有自己的命令列表，从而导致关于哪个列表执行的模糊性。


If the first command you specify in a command list is `silent`, the usual message about stopping at a breakpoint is not printed. This may be desirable for breakpoints that are to print a specific message and then continue. If none of the remaining commands print anything, you see no sign that the breakpoint was reached. `silent` is meaningful only at the beginning of a breakpoint command list.

> 如果在命令列表中指定的第一个命令是“silent”，则不会打印有关在断点处停止的常规消息。 对于要打印特定消息并继续的断点，这可能是可取的。 如果剩余的命令没有打印任何内容，则您看不到到达断点的任何迹象。 “silent”仅在断点命令列表的开头有意义。


The commands `echo`, `output`, and `printf` allow you to print precisely controlled output, and are often useful in silent breakpoints. See [Commands for Controlled Output](Output.html#Output).

> 命令`echo`、`output`和`printf`可以让你输出精确控制的输出，在静默断点处经常很有用。参见[控制输出的命令](Output.html#Output)。


For example, here is how you could use breakpoint commands to print the value of `x` at entry to `foo` whenever `x` is positive.

> 例如，您可以使用断点命令来打印`x`在进入`foo`时的值，只要`x`为正数。

::: smallexample

```bash
break foo if x>0
commands
silent
printf "x is %d\n",x
cont
end
```

:::


One application for breakpoint commands is to compensate for one bug so you can test for another. Put a breakpoint just after the erroneous line of code, give it a condition to detect the case in which something erroneous has been done, and give it commands to assign correct values to any variables that need them. End with the `continue` command so that your program does not stop, and start with the `silent` command so that no output is produced. Here is an example:

> 一个用于断点命令的应用是为了补偿一个错误，以便你可以测试另一个。在错误的代码行之后放置一个断点，给它一个条件来检测发生错误的情况，并给它命令来为需要的变量赋予正确的值。以`continue`命令结束，以便你的程序不会停止，并以`silent`命令开头，以便不产生输出。这里有一个例子：

::: smallexample

```bash
break 403
commands
silent
set x = y + 4
cont
end
```

:::

---

::: header
Next: [Dynamic Printf](Dynamic-Printf.html#Dynamic-Printf)]
:::
