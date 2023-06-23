---
tip: translate by openai@2023-06-23 13:14:13
...
---
description: Shell Commands (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Shell Commands (Debugging with GDB)
lang: en
resource-type: document
title: Shell Commands (Debugging with GDB)
---
::: header
Next: [Logging Output](Logging-Output.html#Logging-Output)]
:::

---

### 2.3 Shell Commands


If you need to execute occasional shell commands during your debugging session, there is no need to leave or suspend [GDB]; you can just use the `shell` command.

> 如果在调试过程中需要执行偶尔的shell命令，无需离开或暂停[GDB]，只需使用`shell`命令即可。

`shell command-string`

`!command-string`


Invoke a shell to execute `command-string` on MS-DOS, etc.).

> 在MS-DOS等系统中调用一个Shell来执行`command-string`。


You may also invoke shell commands from expressions, using the `$_shell` convenience function. See [\$_shell convenience function](Convenience-Funs.html#g_t_0024_005fshell-convenience-function).

> 您也可以从表达式中调用shell命令，使用`$_shell`便捷功能。请参阅[$_shell便捷功能](Convenience-Funs.html#g_t_0024_005fshell-convenience-function)。


The utility `make` is often needed in development environments. You do not have to use the `shell` command for this purpose in [GDB]:

> 在开发环境中经常需要使用`make`工具。在GDB中不需要使用`shell`命令来完成这个目的。

`make make-args`


Execute the `make` program with the specified arguments. This is equivalent to '`shell make make-args`'.

> 执行 `make` 程序，使用指定的参数。这相当于 '`shell make make-args`'。

`pipe [command] | shell_command`

`| [command] | shell_command`

`pipe -d delim command delim shell_command`

`| -d delim command delim shell_command`


Executes `command` is provided, the last command executed is repeated.

> 如果提供了`命令`，则执行该命令；如果没有提供，则重复执行上一条命令。

In case the `command`.

Example:

::: smallexample

```bash
(gdb) p var
$1 = {
  black = 144,
  red = 233,
  green = 377,
  blue = 610,
  white = 987
}
```

```bash
(gdb) pipe p var|wc
      7      19      80
(gdb) |p var|wc -l
7
```

```bash
(gdb) p /x var
$4 = {
  black = 0x90,
  red = 0xe9,
  green = 0x179,
  blue = 0x262,
  white = 0x3db
}
(gdb) ||grep red
  red => 0xe9,
```

```bash
(gdb) | -d ! echo this contains a | char\n ! sed -e 's/|/PIPE/'
this contains a PIPE char
(gdb) | -d xxx echo this contains a | char!\n xxx sed -e 's/|/PIPE/'
this contains a PIPE char!
(gdb)
```

:::


The convenience variables `$_shell_exitcode` and `$_shell_exitsignal` can be used to examine the exit status of the last shell command launched by `shell`, `make`, `pipe` and `|`. See [Convenience Variables](Convenience-Vars.html#Convenience-Vars).

> 可以使用便利变量`$_shell_exitcode`和`$_shell_exitsignal`来检查由`shell`、`make`、`pipe`和`|`启动的最后一个shell命令的退出状态。请参见[便利变量](Convenience-Vars.html#Convenience-Vars)。

---

::: header
Next: [Logging Output](Logging-Output.html#Logging-Output)]
:::
