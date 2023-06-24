---
tip: translate by openai@2023-06-23 19:04:02
...
---
description: Command History (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Command History (Debugging with GDB)
lang: en
resource-type: document
title: Command History (Debugging with GDB)
---
::: header
Next: [Screen Size](Screen-Size.html#Screen-Size)]
:::

---

### 22.3 Command History


[GDB] command history facility.

> [GDB] 命令历史记录设施。


[GDB] History library, a part of the Readline package, to provide the history facility. See [Using History Interactively](Using-History-Interactively.html#Using-History-Interactively), for the detailed description of the History library.

> [GDB] 历史库是Readline包的一部分，提供历史记录功能。详细描述请参见[交互式使用历史记录](Using-History-Interactively.html#Using-History-Interactively)。


To issue a command to [GDB]'s notion of which command to repeat if RET is pressed on a line by itself.

> 给GDB发出一个命令，以决定如果在一行上按下RET，要重复哪个命令。


The server prefix does not affect the recording of values into the value history; to print a value without recording it into the value history, use the `output` command instead of the `print` command.

> 服务器前缀不会影响将值记录到值历史中；要打印一个值而不将其记录到值历史中，请使用`output`命令而不是`print`命令。


Here is the description of [GDB] commands related to command history.

> 以下是有关命令历史的GDB命令的描述。

`set history filename [fname]`


Set the name of the [GDB] on MS-DOS) if this variable is not set.

> 若未设置[GDB]的名称，请在MS-DOS上设置该变量。


The `GDBHISTFILE` environment variable is read after processing any [GDB] initialization files (see [Startup](Startup.html#Startup)) and after processing any commands passed using command line options (for example, `-ex`).

> 环境变量GDBHISTFILE在处理任何GDB初始化文件（参见启动）以及处理使用命令行选项（例如，-ex）传递的任何命令之后读取。


If the `fname` will neither try to load an existing history file, nor will it try to save the history on exit.

> 如果`fname`不尝试加载现有的历史文件，也不会在退出时尝试保存历史记录。

`set history save`

`set history save on`


Record command history in a file, whose name may be specified with the `set history filename` command. By default, this option is disabled. The command history will be recorded when [GDB] exits. If `set history filename` is set to the empty string then history saving is disabled, even when `set history save` is `on`.

> 记录命令历史记录到一个文件中，文件名可以通过`set history filename`命令指定。默认情况下，该选项被禁用。当[GDB]退出时，命令历史将被记录。如果`set history filename`被设置为空字符串，即使`set history save`设置为`on`，历史保存也被禁用。

`set history save off`


Don't record the command history into the file specified by `set history filename` when [GDB] exits.

> 不要在[GDB]退出时将命令历史记录保存到`set history filename`指定的文件中。

`set history size size`

`set history size unlimited`


Set the number of commands which [GDB] keeps in the history list is unlimited.

> 设置[GDB]保存在历史列表中的命令数量为无限制。


The `GDBHISTSIZE` environment variable is read after processing any [GDB] initialization files (see [Startup](Startup.html#Startup)) and after processing any commands passed using command line options (for example, `-ex`).

> 环境变量GDBHISTSIZE在处理任何GDB初始化文件（参见启动）以及处理使用命令行选项（例如-ex）传递的任何命令之后读取。

`set history remove-duplicates count`

`set history remove-duplicates unlimited`


Control the removal of duplicate history entries in the command history list. If `count` is 0, then removal of duplicate history entries is disabled.

> 控制命令历史列表中重复历史记录的移除。如果`count`为0，则禁用重复历史记录的移除。


Only history entries added during the current session are considered for removal. This option is set to 0 by default.

> 只有在当前会话期间添加的历史记录才会被考虑删除。此选项默认设置为0。


History expansion assigns special meaning to the character [!]. See [Event Designators](Event-Designators.html#Event-Designators), for more details.

> 历史展开为特殊字符[!]赋予了特殊含义。有关更多细节，请参阅[事件指示器](Event-Designators.html#Event-Designators)。


Since [!], even when history expansion is enabled.

> 自从[！],即使历史扩展被启用了也是如此。


The commands to control history expansion are:

> 控制历史展开的命令是：

`set history expansion on`
`set history expansion`

:

```
Enable history expansion. History expansion is off by default.
```

`set history expansion off`


:   Disable history expansion.

> 禁用历史扩展。

```

```

`show history`
`show history filename`
`show history save`
`show history size`
`show history expansion`


:   These commands display the state of the [GDB] history parameters. `show history` by itself displays all four states.

> 这些命令显示[GDB]历史参数的状态。只需输入`show history`就可以显示所有四种状态。

`show commands`


Display the last ten commands in the command history.

> 顯示命令歷史中的最後十個命令。

`show commands n`


Print ten commands centered on command number `n`.

> 打印以第n条命令为中心的十条命令

`show commands +`


Print ten commands just after the commands last printed.

> 打印最后一次打印的命令之后的十个命令。

---

::: header
Next: [Screen Size](Screen-Size.html#Screen-Size)]
:::
