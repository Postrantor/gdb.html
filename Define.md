---
tip: translate by openai@2023-06-23 20:28:49
...
---
description: Define (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Define (Debugging with GDB)
lang: en
resource-type: document
title: Define (Debugging with GDB)
---
::: header
Next: [Hooks](Hooks.html#Hooks)]
:::

---

#### 23.1.1 User-defined Commands


A *user-defined command* is a sequence of [GDB] commands to which you assign a new name as a command. This is done with the `define` command. User commands may accept an unlimited number of arguments separated by whitespace. Arguments are accessed within the user command via `$arg0…$argN`. A trivial example:

> 一个*用户定义的命令*是一系列[GDB]命令，您可以将其分配给一个新的名称作为命令。这是通过`define`命令完成的。用户命令可以接受无限数量的由空格分隔的参数。参数在用户命令中通过`$arg0…$argN`访问。一个简单的例子：

::: smallexample

```bash
define adder
  print $arg0 + $arg1 + $arg2
end
```

:::

To execute the command use:

::: smallexample

```bash
adder 1 2 3
```

:::


This defines the command `adder`, which prints the sum of its three arguments. Note the arguments are text substitutions, so they may reference variables, use complex expressions, or even perform inferior functions calls.

> 这定义了命令`adder`，它会打印三个参数的和。注意参数是文本替换，因此它们可以引用变量、使用复杂表达式，甚至执行更低级别的函数调用。


In addition, `$argc` may be used to find out how many arguments have been passed.

> 此外，可以使用`$argc`来查看传递了多少参数。

::: smallexample

```bash
define adder
  if $argc == 2
    print $arg0 + $arg1
  end
  if $argc == 3
    print $arg0 + $arg1 + $arg2
  end
end
```

:::


Combining with the `eval` command (see [eval](Output.html#eval)) makes it easier to process a variable number of arguments:

> 结合`eval`命令（参见[eval]（Output.html#eval））可以更容易地处理可变数量的参数：

::: smallexample

```bash
define adder
  set $i = 0
  set $sum = 0
  while $i < $argc
    eval "set $sum = $sum + $arg%d", $i
    set $i = $i + 1
  end
  print $sum
end
```

:::

`define commandname`

Define a command named `commandname`' command.


The definition of the command is made up of other [GDB] command lines, which are given following the `define` command. The end of these commands is marked by a line containing `end`.

> 命令的定义由其他[GDB]命令行组成，这些命令行在`define`命令之后给出。这些命令的结尾由一行包含`end`的行标记。

`document commandname`


Document the user-defined command `commandname` displays the documentation you have written.

> 命令 `commandname` 显示您已经编写的文档，这是一个用户定义的命令。


You may use the `document` command again to change the documentation of a command. Redefining the command with `define` does not change the documentation.

> 你可以再次使用`document`命令来更改命令的文档。使用`define`重新定义命令不会更改文档。


It is also possible to document user-defined aliases. The alias documentation will then be used by the `help` and `apropos` commands instead of the documentation of the aliased command. Documenting a user-defined alias is particularly useful when defining an alias as a set of nested `with` commands (see [Command aliases default args](Command-aliases-default-args.html#Command-aliases-default-args)).

> 也可以文档化用户定义的别名。然后，别名文档将由`help`和`apropos`命令使用，而不是别名命令的文档。当定义别名为一组嵌套的`with`命令时，文档化用户定义的别名尤其有用（请参阅[命令别名默认参数](Command-aliases-default-args.html#Command-aliases-default-args)）。

`define-prefix commandname`

Define or mark the command `commandname` indicates so to the user).

Example:

::: example

```example
(gdb) define-prefix abc
(gdb) define-prefix abc def
(gdb) define abc def
Type commands for definition of "abc def".
End with a line saying just "end".
>echo command initial def\n
>end
(gdb) define abc def ghi
Type commands for definition of "abc def ghi".
End with a line saying just "end".
>echo command ghi\n
>end
(gdb) define abc def
Keeping subcommands of prefix command "def".
Redefine command "def"? (y or n) y
Type commands for definition of "abc def".
End with a line saying just "end".
>echo command def\n
>end
(gdb) abc def ghi
command ghi
(gdb) abc def
command def
(gdb)
```

:::

`dont-repeat`


Used inside a user-defined command, this tells [GDB] that this command should not be repeated when the user hits RET (see [repeat last command](Command-Syntax.html#Command-Syntax)).

> 在用户定义的命令中使用，这告诉[GDB]，当用户按下RET时，不应重复此命令（参见[重复上一条命令]（Command-Syntax.html#Command-Syntax））。

`help user-defined`


List all user-defined commands and all python commands defined in class COMMAND_USER. The first line of the documentation or docstring is included (if any).

> 列出所有用户定义的命令和在类COMMAND_USER中定义的所有Python命令。包括文档或文档字符串的第一行（如果有的话）。

`show user`

`show user commandname`


Display the [GDB] is given, display the definitions for all user-defined commands. This does not work for user-defined python commands.

> 显示给定的[GDB]，显示所有用户定义的命令的定义。这不适用于用户定义的python命令。

`show max-user-call-depth`

`set max-user-call-depth`


The value of `max-user-call-depth` controls how many recursion levels are allowed in user-defined commands before [GDB] suspects an infinite recursion and aborts the command. This does not apply to user-defined python commands.

> `max-user-call-depth` 的值控制用户定义的命令可以允许多少层递归，在此之前，[GDB] 会怀疑是无限递归，并中止该命令。这不适用于用户定义的python命令。


In addition to the above commands, user-defined commands frequently use control flow commands, described in [Command Files](Command-Files.html#Command-Files).

> 除了上述命令之外，用户定义的命令经常使用控制流命令，详见[命令文件](Command-Files.html#Command-Files)。


When user-defined commands are executed, the commands of the definition are not printed. An error in any command stops execution of the user-defined command.

> 当执行用户定义的命令时，不会打印定义的命令。 任何命令中的错误都会停止执行用户定义的命令。


If used interactively, commands that would ask for confirmation proceed without asking when used inside a user-defined command. Many [GDB] commands that normally print messages to say what they are doing omit the messages when used in a user-defined command.

> 如果在交互式使用时，会要求确认的命令，在用户定义的命令中使用时则不会再次询问。许多[GDB]命令通常会打印一些信息来描述它们正在做什么，但在用户定义的命令中使用时则会省略这些信息。

---

::: header
Next: [Hooks](Hooks.html#Hooks)]
:::
