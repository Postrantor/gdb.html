---
tip: translate by openai@2023-06-23 20:46:50
...
---
description: Emacs (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Emacs (Debugging with GDB)
lang: en
resource-type: document
title: Emacs (Debugging with GDB)
---
::: header
Next: [GDB/MI](GDB_002fMI.html#GDB_002fMI)]
:::

---

## 26 Using [GDB]

A special interface allows you to use [GNU].


To use this interface, use the command [M-x gdb] as a subprocess of Emacs, with input and output through a newly created Emacs buffer.

> 使用这个界面，请在Emacs中使用命令[M-x gdb]作为子进程，并通过一个新创建的Emacs缓冲区输入和输出。

Running [GDB] normally except for two things:

- All "terminal" input and output goes through an Emacs buffer, called the GUD buffer.


  This applies both to [GDB] commands and their output, and to the input and output done by the program you are debugging.

> 这同样适用于[GDB]命令及其输出，以及您正在调试的程序的输入和输出。


  This is useful because it means that you can copy the text of previous commands and input them again; you can even use parts of the output in this way.

> 这很有用，因为它意味着你可以复制以前命令的文本，然后再次输入它们；你甚至可以用这种方式使用输出的一部分。


  All the facilities of Emacs' Shell mode are available for interacting with your program. In particular, you can send signals the usual way---for example, [C-c C-c] for a stop.

> 所有Emacs的Shell模式的功能都可以用来与您的程序交互。特别是，您可以以通常的方式发送信号，例如[C-c C-c]表示停止。
- [GDB] displays source code through Emacs.

  Each time [GDB] session and the source.


  Explicit [GDB] `list` or search commands still produce output as usual, but you probably have no reason to use them from Emacs.

> 显式的[GDB] `list`或搜索命令仍然会产生正常的输出，但你可能没有理由从Emacs中使用它们。


We call this *text command mode*. Emacs 22.1, and later, also uses a graphical mode, enabled by default, which provides further buffers that can control the execution and describe the state of your program. See [GDB Graphical Interface](../Emacs/GDB-Graphical-Interface.html#GDB-Graphical-Interface) in The [GNU] Emacs Manual.

> 我们称之为“文本命令模式”。Emacs 22.1及以后的版本也使用了默认启用的图形模式，它提供了更多的缓冲区来控制程序的执行和描述程序的状态。请参见[GNU] Emacs手册中的[GDB图形界面](../Emacs/GDB-Graphical-Interface.html#GDB-Graphical-Interface)。


If you specify an absolute file name when prompted for the [M-x gdb] input and output session proceeds normally, the auxiliary buffer does not display the current source and line of execution.

> 如果在[M-x gdb]输入提示时指定绝对文件名，输入输出会正常进行，辅助缓冲区不会显示当前源代码和执行行。


The initial working directory of [GDB] to operate on. See [Commands to Specify Files](Files.html#Files).

> 初始工作目录用于[GDB]操作。请参阅[指定文件命令](Files.html#Files)。


By default, [M-x gdb] by a different name (for example, if you keep several configurations around, with different names) you can customize the Emacs variable `gud-gdb-command-name` to run the one you want.

> 默认情况下，可以通过自定义Emacs变量`gud-gdb-command-name`来以不同的名称运行[M-x gdb]（例如，如果你有几个不同名称的配置），以运行所需的配置。


In the GUD buffer, you can use these special Emacs commands in addition to the standard Shell mode commands:

> 在 GUD 缓冲区中，除了标准 Shell 模式命令之外，还可以使用这些特殊的 Emacs 命令：

[C-h m]

:   Describe the features of Emacs' GUD Mode.

[C-c C-s]


:   Execute to another source line, like the [GDB] `step` command; also update the display window to show the current file and location.

> 执行到另一个源代码行，就像[GDB] `step`命令一样；同时更新显示窗口以显示当前文件和位置。

[C-c C-n]


:   Execute to next source line in this function, skipping all function calls, like the [GDB] `next` command. Then update the display window to show the current file and location.

> 执行此函数中的下一源行，跳过所有函数调用，就像[GDB]的`next`命令一样。然后更新显示窗口以显示当前文件和位置。

[C-c C-i]


:   Execute one instruction, like the [GDB] `stepi` command; update display window accordingly.

> 执行一条指令，就像[GDB] `stepi`命令一样；相应地更新显示窗口。

[C-c C-f]


:   Execute until exit from the selected stack frame, like the [GDB] `finish` command.

> 执行直到从选定的堆栈帧退出，就像[GDB] `finish`命令一样。

[C-c C-r]


:   Continue execution of your program, like the [GDB] `continue` command.

> 继续执行你的程序，就像[GDB] `continue`命令一样。

[C-c \<]


:   Go up the number of frames indicated by the numeric argument (see [Numeric Arguments](../Emacs/Arguments.html#Arguments) in The [GNU] `up` command.

> 输入数字参数（参见[数字参数]（../Emacs/Arguments.html#Arguments），按[GNU] `up` 命令上移指定的帧数。

[C-c \>]


:   Go down the number of frames indicated by the numeric argument, like the [GDB] `down` command.

> 下降按照数字参数指定的帧数，就像[GDB] `down` 命令一样。


In any source file, the Emacs command [C-x [SPC] to set a breakpoint on the source line point is on.

> 在任何源文件中，使用Emacs命令[C-x [SPC] 可以在当前行设置断点。


In text command mode, if you type [M-x speedbar] to make the selected frame become the current one. In graphical mode, the speedbar displays watch expressions.

> 在文本命令模式下，输入[M-x speedbar]可以使选中的框架变成当前框架。在图形模式下，speedbar显示监视表达式。


If you accidentally delete the source-display buffer, an easy way to get it back is to type the command `f` in the [GDB] buffer, to request a frame display; when you run under Emacs, this recreates the source buffer if necessary to show you the context of the current frame.

> 如果您不小心删除了源显示缓冲区，一种简单的方法是在[GDB]缓冲区中输入命令`f`，以请求帧显示；当您在Emacs下运行时，如果有必要，它会重新创建源缓冲区，以向您显示当前帧的上下文。


The source files displayed in Emacs are in ordinary Emacs buffers which are visiting the source files in the usual way. You can edit the files with these buffers if you wish; but keep in mind that [GDB] knows cease to correspond properly with the code.

> Emacs中显示的源文件是按照通常的方式访问源文件的普通Emacs缓冲区。如果你愿意，你可以用这些缓冲区编辑文件；但是要记住，[GDB]可能不再与代码保持一致。


A more detailed description of Emacs' interaction with [GDB] Emacs Manual).

> 关于Emacs与GDB的更详细的描述（参见Emacs手册）。

---

::: header
Next: [GDB/MI](GDB_002fMI.html#GDB_002fMI)]
:::
