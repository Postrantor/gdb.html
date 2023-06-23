---
description: Command aliases default args (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Command aliases default args (Debugging with GDB)
lang: en
resource-type: document
title: Command aliases default args (Debugging with GDB)
---
::: header
Up: [Aliases](Aliases.html#Aliases)]
:::

---

#### 23.2.1 Default Arguments

You can tell [GDB] to always prepend some default arguments to the list of arguments provided explicitly by the user when using a user-defined alias.

If you repeatedly use the same arguments or options for a command, you can define an alias for this command and tell [GDB].

For example, if you often use the command `thread apply all` specifying to work on the threads in ascending order and to continue in case it encounters an error, you can tell [GDB] to automatically preprend the `-ascending` and `-c` options by using:

::: smallexample

```bash
(gdb) alias thread apply asc-all = thread apply all -ascending -c
```

:::

Once you have defined this alias with its default args, any time you type the `thread apply asc-all` followed by `some arguments`, [GDB] will execute `thread apply all -ascending -c some arguments`.

To have even less to type, you can also define a one word alias:

::: smallexample

```bash
(gdb) alias t_a_c = thread apply all -ascending -c
```

:::

As usual, unambiguous abbreviations can be used for `alias`.

The different aliases of a command do not share their default args. For example, you define a new alias `bt_ALL` showing all possible information and another alias `bt_SMALL` showing very limited information using:

::: smallexample

```bash
(gdb) alias bt_ALL = backtrace -entry-values both -frame-arg all \
   -past-main -past-entry -full
(gdb) alias bt_SMALL = backtrace -entry-values no -frame-arg none \
   -past-main off -past-entry off
```

:::

(For more on using the `alias` command, see [Aliases](Aliases.html#Aliases).)

Default args are not limited to the arguments and options of `command` accepts such a nested command as argument. For example, the below defines `faalocalsoftype` that lists the frames having locals of a certain type, together with the matching local vars:

::: smallexample

```bash
(gdb) alias faalocalsoftype = frame apply all info locals -q -t
(gdb) faalocalsoftype int
#1  0x55554f5e in sleeper_or_burner (v=0xdf50) at sleepers.c:86
i = 0
ret = 21845
```

:::

This is also very useful to define an alias for a set of nested `with` commands to have a particular combination of temporary settings. For example, the below defines the alias `pp10` that pretty prints an expression argument, with a maximum of 10 elements if the expression is a string or an array:

::: smallexample

```bash
(gdb) alias pp10 = with print pretty -- with print elements 10 -- print
```

:::

This defines the alias `pp10` as being a sequence of 3 commands. The first part `with print pretty --` temporarily activates the setting `set print pretty`, then launches the command that follows the separator `--`. The command following the first part is also a `with` command that temporarily changes the setting `set print elements` to 10, then launches the command that follows the second separator `--`. The third part `print` is the command the `pp10` alias will launch, using the temporary values of the settings and the arguments explicitly given by the user. For more information about the `with` command usage, see [Command Settings](Command-Settings.html#Command-Settings).

By default, asking the help for an alias shows the documentation of the aliased command. When the alias is a set of nested commands, `help` of an alias shows the documentation of the first command. This help is not particularly useful for an alias such as `pp10`. For such an alias, it is useful to give a specific documentation using the `document` command (see [document](Define.html#Define)).

::: footnote

---

#### Footnotes

### [(18)](#DOCF18)

[GDB] could easily accept default arguments for pre-defined commands and aliases, but it was deemed this would be confusing, and so is not allowed.
:::

---

::: header
Up: [Aliases](Aliases.html#Aliases)]
:::
