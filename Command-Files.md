---
tip: translate by openai@2023-06-23 19:02:27
...
---
description: Command Files (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Command Files (Debugging with GDB)
lang: en
resource-type: document
title: Command Files (Debugging with GDB)
---
::: header
Next: [Output](Output.html#Output)]
:::

---

#### 23.1.3 Command Files


A command file for [GDB]) may also be included. An empty line in a command file does nothing; it does not mean to repeat the last command, as it would from the terminal.

> 一个[GDB]的命令文件也可以被包含在内。在命令文件中的空行不会做任何事情；它不会像从终端中那样重复上一个命令。


You can request the execution of a command file with the `source` command. Note that the `source` command is also used to evaluate scripts that are not Command Files. The exact behavior can be configured using the `script-extension` setting. See [Extending GDB](Extending-GDB.html#Extending-GDB).

> 你可以使用`source`命令请求执行命令文件。请注意，`source`命令也用于评估不是命令文件的脚本。可以使用`script-extension`设置来配置具体行为。请参阅[扩展GDB](Extending-GDB.html#Extending-GDB)。

`source [-s] [-v] filename`


Execute the command file `filename`.

> 执行命令文件`文件名`。


The lines in a command file are generally executed sequentially, unless the order of execution is changed by one of the *flow-control commands* described below. The commands are not printed as they are executed. An error in any command terminates execution of the command file and control is returned to the console.

> 命令文件中的行通常按顺序执行，除非由下面描述的*流程控制命令*改变执行顺序。命令在执行时不会打印出来。任何命令中的错误都会终止命令文件的执行，控制权返回到控制台。


[GDB] is not searched because the compilation directory is not relevant to scripts.

> [GDB] 不被搜索，因为编译目录与脚本无关。


If `-s` is specified, then [GDB].

> 如果指定了'-s'，那么[GDB]。


If `-v`, for verbose mode, is given then [GDB], and is interpreted as part of the filename anywhere else.

> 如果给出`-v`，即详细模式，则[GDB]会被解释为文件名的一部分。


Commands that would ask for confirmation if used interactively proceed without asking when used in a command file. Many [GDB] commands that normally print messages to say what they are doing omit the messages when called from command files.

> 命令如果在交互式使用时会要求确认，在命令文件中使用时则不会询问。许多[GDB]命令通常会打印消息来说明它们正在做什么，但是从命令文件调用时则省略了这些消息。


[GDB] also accepts command input from standard input. In this mode, normal output goes to standard output and error output goes to standard error. Errors in a command file supplied on standard input do not terminate execution of the command file---execution continues with the next command.

> [GDB] 也接受来自标准输入的命令输入。 在此模式下，正常输出转到标准输出，错误输出转到标准错误。 标准输入提供的命令文件中的错误不会终止命令文件的执行 - 继续执行下一个命令。

::: smallexample

```bash
gdb < cmds > log 2>&1
```

:::


(The syntax above will vary depending on the shell used.) This example will execute commands from the file `cmds`.

> 以上语法会根据使用的shell而有所不同。这个例子将会执行来自文件`cmds`中的命令。


Since commands stored on command files tend to be more general than commands typed interactively, they frequently need to deal with complicated situations, such as different or unexpected values of variables and symbols, changes in how the program being debugged is built, etc. [GDB] provides a set of flow-control commands to deal with these complexities. Using these commands, you can write complex scripts that loop over data structures, execute commands conditionally, etc.

> 由于存储在命令文件中的命令通常比交互式输入的命令更加通用，因此它们经常需要处理复杂的情况，例如变量和符号的不同或意外的值，调试程序的构建方式的变化等。[GDB]提供了一组流程控制命令来处理这些复杂性。使用这些命令，您可以编写循环数据结构、有条件地执行命令等的复杂脚本。

`if`

`else`


This command allows to include in your script conditionally executed commands. The `if` command takes a single argument, which is an expression to evaluate. It is followed by a series of commands that are executed only if the expression is true (its value is nonzero). There can then optionally be an `else` line, followed by a series of commands that are only executed if the expression was false. The end of the list is marked by a line containing `end`.

> 这个命令允许在脚本中有条件地执行命令。`if`命令需要一个参数，即要评估的表达式。然后是一系列命令，只有在表达式为真（其值为非零）时才会执行。然后可以有一个`else`行，其后是一系列只有在表达式为假时才会执行的命令。列表的结尾由一行包含`end`的行标记。

`while`


This command allows to write loops. Its syntax is similar to `if`: the command takes a single argument, which is an expression to evaluate, and must be followed by the commands to execute, one per line, terminated by an `end`. These commands are called the *body* of the loop. The commands in the body of `while` are executed repeatedly as long as the expression evaluates to true.

> 这个命令允许写循环。它的语法类似于`if`：命令需要一个参数，该参数是要评估的表达式，并且必须跟随一行一行要执行的命令，以`end`结尾。这些命令称为循环的*body*。只要表达式的评估结果为真，`while`命令中的命令就会被重复执行。

`loop_break`


This command exits the `while` loop in whose body it is included. Execution of the script continues after that `while` s `end` line.

> 这条命令会退出包含它的`while`循环。脚本在`while`的`end`行之后继续执行。

`loop_continue`


This command skips the execution of the rest of the body of commands in the `while` loop in whose body it is included. Execution branches to the beginning of the `while` loop, where it evaluates the controlling expression.

> 这个命令跳过`while`循环体中剩余的命令的执行。执行转移到`while`循环的开头，在那里它会评估控制表达式。

`end`


Terminate the block of commands that are the body of `if`, `else`, or `while` flow-control commands.

> 终止if、else或while流控制命令的命令块。

---

::: header
Next: [Output](Output.html#Output)]
:::
