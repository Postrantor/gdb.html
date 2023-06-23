---
tip: translate by openai@2023-06-23 12:41:11
...
---
description: Selection (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Selection (Debugging with GDB)
lang: en
resource-type: document
title: Selection (Debugging with GDB)
---
::: header
Next: [Frame Info](Frame-Info.html#Frame-Info)]
:::

---

### 8.3 Selecting a Frame


Most commands for examining the stack and other data in your program work on whichever stack frame is selected at the moment. Here are the commands for selecting a stack frame; all of them finish by printing a brief description of the stack frame just selected.

> 大多数用于检查程序中堆栈和其他数据的命令都可以在当前选定的堆栈帧上运行。以下是用于选择堆栈帧的命令；所有这些命令都会打印出刚刚选择的堆栈帧的简要描述。

`frame [ frame-selection-spec ]`

`f [ frame-selection-spec ]`


The `frame` command allows different stack frames to be selected. The `frame-selection-spec` can be any of the following:

> `frame` 命令允许选择不同的堆栈帧。`frame-selection-spec` 可以是以下之一：

`num`

`level num`


Select frame level `num`. Recall that frame zero is the innermost (currently executing) frame, frame one is the frame that called the innermost one, and so on. The highest level frame is usually the one for `main`.

> 选择框架级别`num`。请记住，第零级框架是最内层（当前正在执行的）框架，第一级框架是调用最内层的框架，依此类推。最高级框架通常是`main`的框架。


As this is the most common method of navigating the frame stack, the string `level` can be omitted. For example, the following two commands are equivalent:

> 这是最常见的导航框架栈的方法，可以省略字符串“level”。例如，以下两个命令是等效的：

::: smallexample

```bash
(gdb) frame 3
(gdb) frame level 3
```

:::

`address stack-address`


Select the frame with stack address `stack-address` for a frame can be seen in the output of `info frame`, for example:

> 选择具有堆栈地址`stack-address`的帧，可以在`info frame`的输出中看到，例如：

::: smallexample

```bash
(gdb) info frame
Stack level 1, frame at 0x7fffffffda30:
 rip = 0x40066d in b (amd64-entry-value.cc:59); saved rip 0x4004c5
 tail call frame, caller of frame at 0x7fffffffda30
 source language c++.
 Arglist at unknown address.
 Locals at unknown address, Previous frame's sp is 0x7fffffffda30
```

:::


The `stack-address` for this frame is `0x7fffffffda30` as indicated by the line:

> 这个帧的堆栈地址为0x7fffffffda30，如行所示：

::: smallexample

```bash
Stack level 1, frame at 0x7fffffffda30:
```

:::

`function function-name`


Select the stack frame for function `function-name` then the inner most stack frame is selected.

> 选择函数`function-name`的堆栈帧，然后会选择最内层的堆栈帧。

`view stack-address [ pc-addr ]`


View a frame that is not part of [GDB].

> 查看不属于[GDB]的帧。


This is useful mainly if the chaining of stack frames has been damaged by a bug, making it impossible for [GDB] to assign numbers properly to all frames. In addition, this can be useful when your program has multiple stacks and switches between them.

> 这主要有用，如果由于某种bug损坏了堆栈帧的链接，使得[GDB]无法正确地为所有帧分配数字，那么这将非常有用。此外，当您的程序具有多个堆栈并在它们之间切换时，这也很有用。


When viewing a frame outside the current backtrace using `frame view` then you can always return to the original stack using one of the previous stack frame selection instructions, for example `frame level 0`.

> 当使用`frame view`查看当前回溯栈外的帧时，您总是可以使用先前的堆栈帧选择指令之一（例如`frame level 0`）返回到原始堆栈。

`up n`


Move `n`, this advances toward the outermost frame, to higher frame numbers, to frames that have existed longer.

> 移动'n'，这会向外最外层框架前进，到更高的帧数，到存在时间更长的帧中。

`down n`


Move `n`, this advances toward the innermost frame, to lower frame numbers, to frames that were created more recently. You may abbreviate `down` as `do`.

> 移动`n`，这会向内层框架前进，到较低的帧号，到最近创建的帧。你可以将`down`缩写为`do`。


All of these commands end by printing two lines of output describing the frame. The first line shows the frame number, the function name, the arguments, and the source file and line number of execution in that frame. The second line shows the text of that source line.

> 所有这些命令最后都会打印出两行输出，描述该框架。第一行显示框架号，函数名，参数以及执行该框架的源文件和行号。第二行显示该源代码行的文本。

For example:

::: smallexample

```bash
(gdb) up
#1  0x22f0 in main (argc=1, argv=0xf7fffbf4, env=0xf7fffbfc)
    at env.c:10
10              read_input_file (argv[i]);
```

:::


After such a printout, the `list` command with no arguments prints ten lines centered on the point of execution in the frame. You can also edit the program at the point of execution with your favorite editing program by typing `edit`. See [Printing Source Lines](List.html#List), for details.

> 在这样的输出之后，如果不带参数地执行`list`命令，就会打印出以当前执行点为中心的十行代码。您也可以通过输入`edit`来使用您喜爱的编辑器在当前执行点处编辑程序。有关详细信息，请参阅[打印源代码行](List.html#List)。

`select-frame [ frame-selection-spec ]`


The `select-frame` command is a variant of `frame` that does not display the new frame after selecting it. This command is intended primarily for use in [GDB] is as for the `frame` command described in [Selecting a Frame](#Selection).

> `select-frame` 命令是 `frame` 命令的一个变体，它在选择新框架后不会显示新框架。该命令主要用于[GDB]，具体参考[选择框架]（#Selection）中描述的`frame`命令。

`up-silently n`

`down-silently n`


These two commands are variants of `up` and `down`, respectively; they differ in that they do their work silently, without causing display of the new frame. They are intended primarily for use in [GDB] command scripts, where the output might be unnecessary and distracting.

> 这两个命令分别是`up`和`down`的变体；它们的不同之处在于它们会无声地完成工作，而不会显示新的帧。它们主要用于[GDB]命令脚本，其中输出可能是不必要的并且会分散注意力。

---

::: header
Next: [Frame Info](Frame-Info.html#Frame-Info)]
:::
