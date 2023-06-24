---
tip: translate by openai@2023-06-23 23:57:25
...
---
description: Logging Output (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Logging Output (Debugging with GDB)
lang: en
resource-type: document
title: Logging Output (Debugging with GDB)
---
::: header
Previous: [Shell Commands](Shell-Commands.html#Shell-Commands)]
:::

---

### 2.4 Logging Output

You may want to save the output of [GDB]'s logging.

`set logging enabled [on|off]`

Enable or disable logging.

`set logging file file`

Change the name of the current logfile. The default logfile is `gdb.txt`.

`set logging overwrite [on|off]`


By default, [GDB] will append to the logfile. Set `overwrite` if you want `set logging enabled on` to overwrite the logfile instead.

> 默认情况下，GDB会追加到日志文件中。如果你想要`set logging enabled on`覆盖日志文件，请设置`overwrite`。

`set logging redirect [on|off]`


By default, [GDB] output will go to both the terminal and the logfile. Set `redirect` if you want output to go only to the log file.

> 默认情况下，[GDB]输出将同时发送到终端和日志文件。如果您只想将输出发送到日志文件，请设置`重定向`。

`set logging debugredirect [on|off]`

By default, [GDB]

`show logging`

Show the current values of the logging settings.


You can also redirect the output of a [GDB] command to a shell command. See [pipe](Shell-Commands.html#pipe).

> 你也可以将GDB命令的输出重定向到shell命令。请参见[pipe](Shell-Commands.html#pipe)。
