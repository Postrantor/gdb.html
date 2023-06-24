---
tip: translate by openai@2023-06-23 17:38:29
...
---
description: Attach (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Attach (Debugging with GDB)
lang: en
resource-type: document
title: Attach (Debugging with GDB)
---
::: header
Next: [Kill Process](Kill-Process.html#Kill-Process)]
:::

---

### 4.7 Debugging an Already-running Process

`attach process-id`


:   This command attaches to a running process---one that was started outside [GDB]' shell command.

> 这个命令连接到一个正在运行的进程---一个是在[GDB]外部启动的。

```
`attach` does not repeat if you press RET a second time after executing the command.
```


To use `attach`, your program must be running in an environment which supports processes; for example, `attach` does not work for programs on bare-board targets that lack an operating system. You must also have permission to send the process a signal.

> 要使用`attach`，您的程序必须在支持进程的环境中运行；例如，缺乏操作系统的裸板目标上的程序不适用`attach`。您还必须有权向该进程发送信号。


When you use `attach`, the debugger finds the program running in the process first by looking in the current working directory, then (if the program is not found) by using the source file search path (see [Specifying Source Directories](Source-Path.html#Source-Path)). You can also use the `file` command to load the program. See [Commands to Specify Files](Files.html#Files).

> 当你使用“attach”时，调试器首先通过查看当前工作目录来查找正在运行的程序，然后（如果没有找到程序），使用源文件搜索路径（参见[指定源目录]（Source-Path.html#Source-Path））。您还可以使用“file”命令加载程序。参见[指定文件的命令]（Files.html#Files）。


If the debugger can determine that the executable file running in the process it is attaching to does not match the current exec-file loaded by [GDB] tries to compare the files by comparing their build IDs (see [build ID](Separate-Debug-Files.html#build-ID)), if available.

> 如果调试器可以确定正在附加到的进程中运行的可执行文件与[GDB]加载的当前exec-file不匹配，它会尝试通过比较它们的构建ID（参见[构建ID]（Separate-Debug-Files.html#build-ID））来比较文件，如果可用。

`set exec-file-mismatch ‘ask|warn|off’`


Whether to detect mismatch between the current executable file loaded by [GDB]', don't attempt to detect a mismatch. If the user confirms loading the process executable file, then its symbols will be loaded as well.

> 不要尝试检测不匹配。如果用户确认加载进程可执行文件，那么它的符号也将被加载。

`show exec-file-mismatch`


Show the current value of `exec-file-mismatch`.

> 显示当前`exec-file-mismatch`的值


The first thing [GDB] to the process.

> 第一件事是给这个过程使用GDB。

`detach`


When you have finished debugging the attached process, you can use the `detach` command to release it from [GDB] become completely independent once more, and you are ready to `attach` another process or start one with `run`. `detach` does not repeat if you press RET again after executing the command.

> 当您完成调试附加的进程后，您可以使用`detach`命令将其从[GDB]中分离，使其再次完全独立，您可以准备`附加`另一个进程或使用`run`开始一个进程。 如果在执行命令后再次按RET，`detach`不会重复。


If you exit [GDB] asks for confirmation if you try to do either of these things; you can control whether or not you need to confirm by using the `set confirm` command (see [Optional Warnings and Messages](Messages_002fWarnings.html#Messages_002fWarnings)).

> 如果你退出GDB，当你尝试做这些事情时它会询问你是否确认；你可以通过使用`set confirm`命令来控制是否需要确认（参见[可选警告和消息](Messages_002fWarnings.html#Messages_002fWarnings)）。

---

::: header
Next: [Kill Process](Kill-Process.html#Kill-Process)]
:::
