---
tip: translate by openai@2023-06-23 19:07:41
...
---
description: Command Settings (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Command Settings (Debugging with GDB)
lang: en
resource-type: document
title: Command Settings (Debugging with GDB)
---
::: header
Next: [Completion](Completion.html#Completion)]
:::

---

### 3.2 Command Settings


Many commands change their behavior according to command-specific variables or settings. These settings can be changed with the `set` subcommands. For example, the `print` command (see [Examining Data](Data.html#Data)) prints arrays differently depending on settings changeable with the commands `set print elements NUMBER-OF-ELEMENTS` and `set print array-indexes`, among others.

> 许多命令会根据特定命令的变量或设置而改变其行为。这些设置可以通过`set`子命令进行更改。例如，`print`命令（参见[检查数据](Data.html#Data)）会根据可以用`set print elements NUMBER-OF-ELEMENTS`和`set print array-indexes`等命令更改的设置来不同方式打印数组。


You can change these settings to your preference in the gdbinit files loaded at [GDB] startup. See [Startup](Startup.html#Startup).

> 你可以在 [GDB] 启动时加载的 gdbinit 文件中按照自己的喜好更改这些设置。参见 [启动](Startup.html#Startup)。


The settings can also be changed interactively during the debugging session. For example, to change the limit of array elements to print, you can do the following:

> 调试会话期间也可以交互式更改设置。例如，要更改要打印的数组元素的限制，可以执行以下操作：

::: smallexample

```bash
(gdb) set print elements 10
(gdb) print some_array
$1 = 
```

:::


The above `set print elements 10` command changes the number of elements to print from the default of 200 to 10. If you only intend this limit of 10 to be used for printing `some_array`, then you must restore the limit back to 200, with `set print elements 200`.

> 上面的`set print elements 10`命令将要打印的元素数量从默认的200个改为10个。如果你只想将10个元素的限制应用于打印`some_array`，那么你必须将限制恢复为200，使用`set print elements 200`。


Some commands allow overriding settings with command options. For example, the `print` command supports a number of options that allow overriding relevant global print settings as set by `set print` subcommands. See [print options](Data.html#print-options). The example above could be rewritten as:

> 一些命令允许使用命令选项覆盖设置。例如，`print` 命令支持许多选项，可以覆盖由 `set print` 子命令设置的相关全局打印设置。请参阅 [print options](Data.html#print-options)。上面的示例可以重写为：

::: smallexample

```bash
(gdb) print -elements 10 -- some_array
$1 = 
```

:::


Alternatively, you can use the `with` command to change a setting temporarily, for the duration of a command invocation.

> 你也可以使用 `with` 命令来暂时改变一个设置，以持续一个命令的调用。

`with setting [value] [-- command]`

`w setting [value] [-- command]`


Temporarily set `setting`.

> 暂时设置“设置”。

`setting` is the value to assign to `setting` while running `command`.


If no `command` is provided, the last command executed is repeated.

> 如果没有提供`命令`，则重复执行上一条命令。


If a `command` is provided, it must be preceded by a double dash (`--`) separator. This is required because some settings accept free-form arguments, such as expressions or filenames.

> 如果提供了一个`命令`，必须在它前面加上双破折号（`--`）分隔符。这是必需的，因为一些设置接受自由形式的参数，例如表达式或文件名。


For example, the command

> 例如，命令

::: smallexample

```bash
(gdb) with print array on -- print some_array
```

:::


is equivalent to the following 3 commands:

> 这相当于以下3个命令：

::: smallexample

```bash
(gdb) set print array on
(gdb) print some_array
(gdb) set print array off
```

:::


The `with` command is particularly useful when you want to override a setting while running user-defined commands, or commands defined in Python or Guile. See [Extending GDB](Extending-GDB.html#Extending-GDB).

> `命令`with`特别有用，当您想要在运行用户定义的命令或在Python或Guile中定义的命令时覆盖设置。请参阅[扩展GDB](Extending-GDB.html#Extending-GDB)。`

::: smallexample

```bash
(gdb) with print pretty on -- my_complex_command
```

:::


To change several settings for the same command, you can nest `with` commands. For example, `with language ada -- with print elements 10` temporarily changes the language to Ada and sets a limit of 10 elements to print for arrays and strings.

> 要为同一个命令更改多个设置，可以嵌套使用`with`命令。例如，`with language ada -- with print elements 10`会暂时把语言更改为Ada，并为数组和字符串设置一个打印元素上限为10。

---

::: header
Next: [Completion](Completion.html#Completion)]
:::
