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

`commands [list…]`

`… command-list …`

`end`

Specify a list of commands for the given breakpoints. The commands themselves appear on the following lines. Type a line containing just `end` to terminate the commands.

To remove all commands from a breakpoint, type `commands` and follow it immediately with `end`; that is, give no commands.

With no argument, `commands` refers to the last breakpoint, watchpoint, or catchpoint set (not to the breakpoint most recently encountered). If the most recent breakpoints were set with a single command, then the `commands` will apply to all the breakpoints set by that command. This applies to breakpoints set by `rbreak`, and also applies when a single `break` command creates multiple breakpoints (see [Ambiguous Expressions](Ambiguous-Expressions.html#Ambiguous-Expressions)).

Pressing RET as a means of repeating the last [GDB].

Inside a command list, you can use the command [disable \$_hit_bpnum] to disable the encountered breakpoint.

If your breakpoint has several code locations, the command [disable \$_hit_bpnum.\$_hit_locno] will disable the specific breakpoint code location encountered. If the breakpoint has only one location, this command will disable the encountered breakpoint.

You can use breakpoint commands to start your program up again. Simply use the `continue` command, or `step`, or any other command that resumes execution.

Any other commands in the command list, after a command that resumes execution, are ignored. This is because any time you resume execution (even with a simple `next` or `step`), you may encounter another breakpoint---which could have its own command list, leading to ambiguities about which list to execute.

If the first command you specify in a command list is `silent`, the usual message about stopping at a breakpoint is not printed. This may be desirable for breakpoints that are to print a specific message and then continue. If none of the remaining commands print anything, you see no sign that the breakpoint was reached. `silent` is meaningful only at the beginning of a breakpoint command list.

The commands `echo`, `output`, and `printf` allow you to print precisely controlled output, and are often useful in silent breakpoints. See [Commands for Controlled Output](Output.html#Output).

For example, here is how you could use breakpoint commands to print the value of `x` at entry to `foo` whenever `x` is positive.

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
