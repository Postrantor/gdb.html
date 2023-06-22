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

You can request the execution of a command file with the `source` command. Note that the `source` command is also used to evaluate scripts that are not Command Files. The exact behavior can be configured using the `script-extension` setting. See [Extending GDB](Extending-GDB.html#Extending-GDB).

`source [-s] [-v] filename`

Execute the command file `filename`.

The lines in a command file are generally executed sequentially, unless the order of execution is changed by one of the *flow-control commands* described below. The commands are not printed as they are executed. An error in any command terminates execution of the command file and control is returned to the console.

[GDB] is not searched because the compilation directory is not relevant to scripts.

If `-s` is specified, then [GDB].

If `-v`, for verbose mode, is given then [GDB], and is interpreted as part of the filename anywhere else.

Commands that would ask for confirmation if used interactively proceed without asking when used in a command file. Many [GDB] commands that normally print messages to say what they are doing omit the messages when called from command files.

[GDB] also accepts command input from standard input. In this mode, normal output goes to standard output and error output goes to standard error. Errors in a command file supplied on standard input do not terminate execution of the command file---execution continues with the next command.

::: smallexample

```bash
gdb < cmds > log 2>&1
```

:::

(The syntax above will vary depending on the shell used.) This example will execute commands from the file `cmds`.

Since commands stored on command files tend to be more general than commands typed interactively, they frequently need to deal with complicated situations, such as different or unexpected values of variables and symbols, changes in how the program being debugged is built, etc. [GDB] provides a set of flow-control commands to deal with these complexities. Using these commands, you can write complex scripts that loop over data structures, execute commands conditionally, etc.

`if`

`else`

This command allows to include in your script conditionally executed commands. The `if` command takes a single argument, which is an expression to evaluate. It is followed by a series of commands that are executed only if the expression is true (its value is nonzero). There can then optionally be an `else` line, followed by a series of commands that are only executed if the expression was false. The end of the list is marked by a line containing `end`.

`while`

This command allows to write loops. Its syntax is similar to `if`: the command takes a single argument, which is an expression to evaluate, and must be followed by the commands to execute, one per line, terminated by an `end`. These commands are called the *body* of the loop. The commands in the body of `while` are executed repeatedly as long as the expression evaluates to true.

`loop_break`

This command exits the `while` loop in whose body it is included. Execution of the script continues after that `while` s `end` line.

`loop_continue`

This command skips the execution of the rest of the body of commands in the `while` loop in whose body it is included. Execution branches to the beginning of the `while` loop, where it evaluates the controlling expression.

`end`

Terminate the block of commands that are the body of `if`, `else`, or `while` flow-control commands.

---

::: header
Next: [Output](Output.html#Output)]
:::
