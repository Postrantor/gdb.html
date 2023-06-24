---
tip: translate by openai@2023-06-24 00:27:10
...
---
description: Mode Options (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Mode Options (Debugging with GDB)
lang: en
resource-type: document
title: Mode Options (Debugging with GDB)
---
::: header
Next: [Startup](Startup.html#Startup)]
:::

---

#### 2.1.2 Choosing Modes


You can run [GDB] in various alternative modes---for example, in batch mode or quiet mode.

> 你可以在各种不同的模式中运行GDB---例如，批处理模式或安静模式。

`-nx`

`-n`


Do not execute commands found in any initialization files (see [Initialization Files](Initialization-Files.html#Initialization-Files)).

> 不要执行任何初始化文件中找到的命令（请参阅[初始化文件]（Initialization-Files.html#Initialization-Files））。

`-nh`


Do not execute commands found in any home directory initialization file (see [Home directory initialization file](Initialization-Files.html#Initialization-Files)). The system wide and current directory initialization files are still loaded.

> 不要执行任何主目录初始化文件中的命令（参见[主目录初始化文件]（Initialization-Files.html#Initialization-Files））。系统范围和当前目录的初始化文件仍然会被加载。

`-quiet`

`-silent`

`-q`


"Quiet". Do not print the introductory and copyright messages. These messages are also suppressed in batch mode.

> 安静。不要打印介绍和版权信息。在批处理模式下也会屏蔽这些信息。


This can also be enabled using `set startup-quietly on`. The default is `off`. Use `show startup-quietly` to see the current setting. Place `set startup-quietly on` into your early initialization file (see [Initialization Files](Initialization-Files.html#Initialization-Files)) to have future [GDB] sessions startup quietly.

> 可以使用“set startup-quietly on”来启用它。默认是关闭的。使用“show startup-quietly”查看当前设置。将“set startup-quietly on”放入您的早期初始化文件（参见[初始化文件]（Initialization-Files.html#Initialization-Files）），以便在未来的[GDB]会话中安静地启动。

`-batch`


Run in batch mode. Exit with status `0` after processing all the command files specified with '`-x` were in effect (see [Messages/Warnings](Messages_002fWarnings.html#Messages_002fWarnings)).

> 以批处理模式运行。在处理完所有使用 '-x' 指定的命令文件后以状态 '0' 退出（参见 [Messages/Warnings](Messages_002fWarnings.html#Messages_002fWarnings)）。


Batch mode may be useful for running [GDB] as a filter, for example to download and run a program on another computer; in order to make this more useful, the message

> 批处理模式可能对运行GDB作为过滤器很有用，例如下载并在另一台计算机上运行程序；为了使其更有用，可以发送消息。

::: smallexample

```bash
Program exited normally.
```

:::


(which is ordinarily issued whenever a program running under [GDB] control terminates) is not issued when running in batch mode.

> 在批处理模式下运行时，不会发出通常在[GDB]控制下运行的程序终止时发出的信号。

`-batch-silent`


Run in batch mode exactly like '`-batch`' and would be useless for an interactive session.

> 以与' -batch'完全相同的批处理模式运行，在交互式会话中毫无用处。


This is particularly useful when using targets that give '`Loading section`' messages, for example.

> 这在使用给出“加载部分”消息的目标时尤其有用。


Note that targets that give their output via [GDB], as opposed to writing directly to `stdout`, will also be made silent.

> 注意，使用[GDB]输出而不是直接写入`stdout`的目标也会变得无声。

`-return-child-result`


The return code from [GDB] will be the return code from the child process (the process being debugged), with the following exceptions:

> GDB的返回代码将是被调试的子进程的返回代码，但有以下例外：

- [GDB]'.
- The user quits with an explicit value. E.g., '`quit 1`'.

- The child process never runs, or is not allowed to terminate, in which case the exit code will be -1.

> 子进程从不运行，或者被禁止终止，在这种情况下，退出代码将为-1。


This option is useful in conjunction with '`-batch` is being used as a remote program loader or simulator interface.

> 这个选项与“-batch”一起使用时，可用于远程程序加载器或模拟器界面。

`-nowindows`

`-nw`


"No windows". If [GDB] to only use the command-line interface. If no GUI is available, this option has no effect.

> "没有窗口"。如果[GDB]只使用命令行界面，如果没有可用的GUI，此选项无效。

`-windows`

`-w`


If [GDB] includes a GUI, then this option requires it to be used if possible.

> 如果GDB包含了GUI，那么这个选项就要求尽可能使用它。

`-cd directory`

Run [GDB] as its working directory, instead of the current directory.

`-data-directory directory`

`-D directory`


Run [GDB] searches for its auxiliary files. See [Data Files](Data-Files.html#Data-Files).

> 运行GDB搜索其辅助文件。请参阅[数据文件](Data-Files.html#Data-Files)。

`-fullname`

`-f`

[GNU]' characters as a signal to display the source code for the frame.

`-annotate level`


This option sets the *annotation level* inside [GDB], and level 2 has been deprecated.

> 这个选项设置[GDB]内的*注释级别*，而第2级已经被弃用。


The annotation mechanism has largely been superseded by [GDB/MI] (see [GDB/MI](GDB_002fMI.html#GDB_002fMI)).

> 注释机制已经大部分被[GDB/MI]（参见[GDB/MI](GDB_002fMI.html#GDB_002fMI)）取代。

`--args`


Change interpretation of command line so that arguments following the executable file are passed as command line arguments to the inferior. This option stops option processing.

> 改变命令行的解释，以便将可执行文件后面的参数作为命令行参数传递给次级。此选项会停止选项处理。

`-baud bps`

`-b bps`


Set the line speed (baud rate or bits per second) of any serial interface used by [GDB] for remote debugging.

> 设置[GDB]用于远程调试的任何串行接口的线速（波特率或比特每秒）。

`-l timeout`


Set the timeout (in seconds) of any communication used by [GDB] for remote debugging.

> 设置 [GDB] 用于远程调试的任何通信的超时（以秒为单位）。

`-tty device`

`-t device`

Run using `device` for your program's standard input and output.

`-tui`


Activate the *Text User Interface* when starting. The Text User Interface manages several text windows on the terminal, showing source, assembly, registers and [GDB] Emacs](Emacs.html#Emacs)).

> 启动时激活文本用户界面。文本用户界面在终端上管理多个文本窗口，显示源代码、汇编、寄存器和[GDB] Emacs](Emacs.html#Emacs))。

`-interpreter interp`


Use the interpreter `interp` using it as a back end. See [Command Interpreters](Interpreters.html#Interpreters).

> 使用`interp`作为后端使用解释器。参见[命令解释器](Interpreters.html#Interpreters)。

'`--interpreter=mi` interfaces are no longer supported.

`-write`


Open the executable and core files for both reading and writing. This is equivalent to the '`set write on` (see [Patching](Patching.html#Patching)).

> 打开可执行文件和核心文件以进行读取和写入。这相当于“set write on”（参见[修补]（Patching.html#Patching））。

`-statistics`


This option causes [GDB] to print statistics about time and memory usage after it completes each command and returns to the prompt.

> 此选项会导致[GDB]在每次命令完成并返回提示符后打印有关时间和内存使用情况的统计信息。

`-version`


This option causes [GDB] to print its version number and no-warranty blurb, and exit.

> 这个选项会导致GDB打印其版本号和无保证声明，然后退出。

`-configuration`

This option causes [GDB] bugs (see [GDB Bugs](GDB-Bugs.html#GDB-Bugs)).

---

::: header
Next: [Startup](Startup.html#Startup)]
:::
