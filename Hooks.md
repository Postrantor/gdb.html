---
tip: translate by openai@2023-06-23 23:08:37
...
---
description: Hooks (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Hooks (Debugging with GDB)
lang: en
resource-type: document
title: Hooks (Debugging with GDB)
---
::: header
Next: [Command Files](Command-Files.html#Command-Files)]
:::

---

#### 23.1.2 User-defined Command Hooks


You may define *hooks*, which are a special kind of user-defined command. Whenever you run the command '`foo`' exists, it is executed (with no arguments) before that command.

> 你可以定义*钩子*，它是一种特殊的用户定义命令。每当你运行命令'`foo`'存在时，它会在该命令之前被执行（无参数）。


A hook may also be defined which is run after the command you executed. Whenever you run the command '`foo`' exists, it is executed (with no arguments) after that command. Post-execution hooks may exist simultaneously with pre-execution hooks, for the same command.

> 当你执行命令'foo'时，也可以定义一个挂钩，它会在你执行的命令之后运行。无论你何时运行命令'foo'，它都会在该命令之后被执行（无需参数）。后期执行挂钩可以与前期执行挂钩同时存在，用于相同的命令。


It is valid for a hook to call the command which it hooks. If this occurs, the hook is not re-executed, thereby avoiding infinite recursion.

> 钩子可以调用其钩子的命令是有效的。如果发生这种情况，钩子不会被重新执行，从而避免无限递归。


In addition, a pseudo-command, '`stop`') makes the associated commands execute every time execution stops in your program: before breakpoint commands are run, displays are printed, or the stack frame is printed.

> 此外，一个伪命令“stop”会使相关命令在程序中每次停止执行时执行：在运行断点命令之前，会打印显示或打印堆栈帧。


For example, to ignore `SIGALRM` signals while single-stepping, but treat them normally during normal execution, you could define:

> 例如，在单步执行时忽略`SIGALRM`信号，但在正常执行时正常处理它们，您可以定义：

::: smallexample

```bash
define hook-stop
handle SIGALRM nopass
end

define hook-run
handle SIGALRM pass
end

define hook-continue
handle SIGALRM pass
end
```

:::


As a further example, to hook at the beginning and end of the `echo` command, and to add extra text to the beginning and end of the message, you could define:

> 作为进一步的例子，在echo命令的开头和结尾挂钩，并在消息的开头和结尾添加额外的文本，您可以定义：

::: smallexample

```bash
define hook-echo
echo <<<---
end

define hookpost-echo
echo --->>>\n
end

(gdb) echo Hello World
<<<---Hello World--->>>
(gdb)
```

:::

You can define a hook for any single-word command in [GDB]'.


If an error occurs during the execution of your hook, execution of [GDB] issues a prompt (before the command that you actually typed had a chance to run).

> 如果在执行你的钩子时发生错误，[GDB] 执行会在你实际输入的命令运行之前发出提示。


If you try to define a hook which does not match any known command, you get a warning from the `define` command.

> 如果您尝试定义一个与任何已知命令不匹配的钩子，您会从“define”命令中得到一个警告。

---

::: header
Next: [Command Files](Command-Files.html#Command-Files)]
:::
