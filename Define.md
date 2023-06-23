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

In addition, `$argc` may be used to find out how many arguments have been passed.

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

`document commandname`

Document the user-defined command `commandname` displays the documentation you have written.

You may use the `document` command again to change the documentation of a command. Redefining the command with `define` does not change the documentation.

It is also possible to document user-defined aliases. The alias documentation will then be used by the `help` and `apropos` commands instead of the documentation of the aliased command. Documenting a user-defined alias is particularly useful when defining an alias as a set of nested `with` commands (see [Command aliases default args](Command-aliases-default-args.html#Command-aliases-default-args)).

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

`help user-defined`

List all user-defined commands and all python commands defined in class COMMAND_USER. The first line of the documentation or docstring is included (if any).

`show user`

`show user commandname`

Display the [GDB] is given, display the definitions for all user-defined commands. This does not work for user-defined python commands.

`show max-user-call-depth`

`set max-user-call-depth`

The value of `max-user-call-depth` controls how many recursion levels are allowed in user-defined commands before [GDB] suspects an infinite recursion and aborts the command. This does not apply to user-defined python commands.

In addition to the above commands, user-defined commands frequently use control flow commands, described in [Command Files](Command-Files.html#Command-Files).

When user-defined commands are executed, the commands of the definition are not printed. An error in any command stops execution of the user-defined command.

If used interactively, commands that would ask for confirmation proceed without asking when used inside a user-defined command. Many [GDB] commands that normally print messages to say what they are doing omit the messages when used in a user-defined command.

---

::: header
Next: [Hooks](Hooks.html#Hooks)]
:::
