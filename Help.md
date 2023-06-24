---
tip: translate by openai@2023-06-23 23:05:34
...
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

> 你可以使用命令'help'随时向GDB本身询问有关其命令的信息。

`help`

`h`


You can use `help` (abbreviated `h`) with no arguments to display a short list of named classes of commands:

> 你可以使用`help`（缩写为`h`）不带参数来显示一个简短的命令类名称列表：

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

> 使用一个常见的帮助类作为参数，您可以获得该类中的各个命令列表。如果命令有别名，则在命令名称后面以逗号分隔列出别名。如果别名有默认参数，则在第一行后面给出别名的完整定义。例如，这是类`状态`的帮助显示：

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

> 使用命令名稱作為`help`參數，[GDB]將顯示以逗號分隔的命令名稱及其所有別名的第一行。此第一行將被具有默認參數的所有別名的完整定義所繼續。在對別名發出幫助請求時，將顯示該別名命令的文檔。


A user-defined alias can optionally be documented using the `document` command (see [document](Define.html#Define)). [GDB] then considers this alias as different from the aliased command: this alias is not listed in the aliased command help output, and asking help for this alias will show the documentation provided for the alias instead of the documentation of the aliased command.

> 用户定义的别名可以选择使用`document`命令进行文档化（详见[document](Define.html#Define)）。GDB会将这个别名与被别名的命令区分开：这个别名不会出现在被别名的命令帮助输出中，而是会显示为为别名提供的文档，而不是被别名的命令的文档。

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

> 结果在下面的输出中，如果启用样式，'thread apply'的剪切会被突出显示。

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

> 命令`complete args`可以列出所有可能的命令开头完成。使用`args`来指定你想要完成的命令的开头。例如：`到`简体中文`

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

> 除了帮助，您还可以使用[GDB]本身。每个命令都支持许多查询主题;本手册将在适当的上下文中介绍它们。在命令、变量和函数索引中的`info`和`show`下的列表指向所有子命令。请参见[命令和变量索引](Command-and-Variable-Index.html#Command-and-Variable-Index)。

`info`


This command (abbreviated `i`) is for describing the state of your program. For example, you can show the arguments passed to a function with `info args`, list the registers currently in use with `info registers`, or list the breakpoints you have set with `info breakpoints`. You can get a complete list of the `info` sub-commands with `help info`.

> 这个命令（缩写为`i`）用于描述程序的状态。例如，可以使用`info args`显示传递给函数的参数，使用`info registers`列出当前使用的寄存器，或使用`info breakpoints`列出设置的断点。您可以使用`help info`获取`info`子命令的完整列表。

`set`


You can assign the result of an expression to an environment variable with `set`. For example, you can set the [GDB] prompt to a \$-sign with `set prompt $`.

> 你可以使用`set`将表达式的结果分配给环境变量。例如，你可以使用`set prompt $`将[GDB]提示符设置为$符号。

`show`


In contrast to `info`, `show` is for describing the state of [GDB] itself. You can change most of the things you can `show`, by using the related command `set`; for example, you can control what number system is used for displays with `set radix`, or simply inquire which is currently in use with `show radix`.

> 相比于`info`，`show`用于描述[GDB]本身的状态。您可以使用相关的命令`set`来更改`show`中的大多数内容；例如，您可以使用`set radix`控制显示哪种数字系统，或者只需使用`show radix`查询当前使用的系统。


To display all the settable parameters and their current values, you can use `show` with no arguments; you may also use `info set`. Both commands produce the same display.

> 要查看所有可设置的参数及其当前值，可以使用不带参数的“show”；也可以使用“info set”。两个命令会产生相同的显示。


Here are several miscellaneous `show` subcommands, all of which are exceptional in lacking corresponding `set` commands:

> 这里有几个不同的`show`子命令，它们都特别的是没有相应的`set`命令：

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

> 显示关于GDB错误的详细信息（请参阅GDB Bugs），将这些信息包含在报告中是非常重要的。

---

::: header
Previous: [Command Options](Command-Options.html#Command-Options)]
:::
