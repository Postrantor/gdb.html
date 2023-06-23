---
description: Help (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Help (Debugging with GDB)
lang: en
resource-type: document
title: Help (Debugging with GDB)
---
::: header
Previous: [Command Options](Command-Options.html#Command-Options)]
:::

---

### 3.5 Getting Help

You can always ask [GDB] itself for information on its commands, using the command `help`.

`help`

`h`

You can use `help` (abbreviated `h`) with no arguments to display a short list of named classes of commands:

::: smallexample

```bash
(gdb) help
List of classes of commands:

aliases -- User-defined aliases of other commands
breakpoints -- Making program stop at certain points
data -- Examining data
files -- Specifying and examining files
internals -- Maintenance commands
obscure -- Obscure features
running -- Running the program
stack -- Examining the stack
status -- Status inquiries
support -- Support facilities
tracepoints -- Tracing of program execution without
               stopping the program
user-defined -- User-defined commands

Type "help" followed by a class name for a list of
commands in that class.
Type "help" followed by command name for full
documentation.
Command name abbreviations are allowed if unambiguous.
(gdb)
```

:::

`help class`

Using one of the general help classes as an argument, you can get a list of the individual commands in that class. If a command has aliases, the aliases are given after the command name, separated by commas. If an alias has default arguments, the full definition of the alias is given after the first line. For example, here is the help display for the class `status`:

::: smallexample

```bash
(gdb) help status
Status inquiries.

List of commands:

info, inf, i -- Generic command for showing things
        about the program being debugged
info address, iamain  -- Describe where symbol SYM is stored.
  alias iamain = info address main
info all-registers -- List of all registers and their contents,
        for selected stack frame.
...
show, info set -- Generic command for showing things
        about the debugger

Type "help" followed by command name for full
documentation.
Command name abbreviations are allowed if unambiguous.
(gdb)
```

:::

`help command`

With a command name as `help` argument, [GDB] will display a first line with the command name and all its aliases separated by commas. This first line will be followed by the full definition of all aliases having default arguments. When asking the help for an alias, the documentation for the aliased command is shown.

A user-defined alias can optionally be documented using the `document` command (see [document](Define.html#Define)). [GDB] then considers this alias as different from the aliased command: this alias is not listed in the aliased command help output, and asking help for this alias will show the documentation provided for the alias instead of the documentation of the aliased command.

`apropos [-v] regexp`

The `apropos` command searches through all of the [GDB]. For example:

::: smallexample

```bash
apropos alias
```

:::

results in:

::: smallexample

```bash
alias -- Define a new command that is an alias of an existing command
aliases -- User-defined aliases of other commands
```

:::

while

::: smallexample

```bash
apropos -v cut.*thread apply
```

:::

results in the below output, where '`cut for 'thread apply`' is highlighted if styling is enabled.

::: smallexample

```bash
taas -- Apply a command to all threads (ignoring errors
and empty output).
Usage: taas COMMAND
shortcut for 'thread apply all -s COMMAND'

tfaas -- Apply a command to all frames of all threads
(ignoring errors and empty output).
Usage: tfaas COMMAND
shortcut for 'thread apply all -s frame apply all -s COMMAND'
```

:::

`complete args`

The `complete args` command lists all the possible completions for the beginning of a command. Use `args` to specify the beginning of the command you want completed. For example:

::: smallexample

```bash
complete i
```

:::

results in:

::: smallexample

```bash
if
ignore
info
inspect
```

:::

This is intended for use by [GNU] Emacs.

In addition to `help`, you can use the [GDB] itself. Each command supports many topics of inquiry; this manual introduces each of them in the appropriate context. The listings under `info` and under `show` in the Command, Variable, and Function Index point to all the sub-commands. See [Command and Variable Index](Command-and-Variable-Index.html#Command-and-Variable-Index).

`info`

This command (abbreviated `i`) is for describing the state of your program. For example, you can show the arguments passed to a function with `info args`, list the registers currently in use with `info registers`, or list the breakpoints you have set with `info breakpoints`. You can get a complete list of the `info` sub-commands with `help info`.

`set`

You can assign the result of an expression to an environment variable with `set`. For example, you can set the [GDB] prompt to a \$-sign with `set prompt $`.

`show`

In contrast to `info`, `show` is for describing the state of [GDB] itself. You can change most of the things you can `show`, by using the related command `set`; for example, you can control what number system is used for displays with `set radix`, or simply inquire which is currently in use with `show radix`.

To display all the settable parameters and their current values, you can use `show` with no arguments; you may also use `info set`. Both commands produce the same display.

Here are several miscellaneous `show` subcommands, all of which are exceptional in lacking corresponding `set` commands:

`show version`

Show what version of [GDB].

`show copying`

`info copying`

Display information about permission for copying [GDB].

`show warranty`

`info warranty`

Display the [GNU] comes with one.

`show configuration`

Display detailed information about the way [GDB] bug (see [GDB Bugs](GDB-Bugs.html#GDB-Bugs)), it is important to include this information in your report.

---

::: header
Previous: [Command Options](Command-Options.html#Command-Options)]
:::
