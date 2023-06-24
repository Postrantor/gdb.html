---
tip: translate by openai@2023-06-23 23:36:10
...
---
description: Invoking GDB (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Invoking GDB (Debugging with GDB)
lang: en
resource-type: document
title: Invoking GDB (Debugging with GDB)
---
::: header
Next: [Quitting GDB](Quitting-GDB.html#Quitting-GDB)]
:::

---

### 2.1 Invoking [GDB]

Invoke [GDB] reads commands from the terminal until you tell it to exit.


You can also run `gdb` with a variety of arguments and options, to specify more of your debugging environment at the outset.

> 你也可以使用各种参数和选项运行`gdb`，以一开始就指定更多的调试环境。


The command-line options described here are designed to cover a variety of situations; in some environments, some of these options may effectively be unavailable.

> 这里描述的命令行选项旨在覆盖各种情况；在某些环境中，其中一些选项可能无法使用。


The most usual way to start [GDB] is with one argument, specifying an executable program:

> 最常见的开始GDB的方法是使用一个参数，指定一个可执行程序：

::: smallexample

```bash
gdb program
```

:::


You can also start with both an executable program and a core file specified:

> 你也可以同时指定一个可执行程序和一个核心文件开始：

::: smallexample

```bash
gdb program core
```

:::


You can, instead, specify a process ID as a second argument or use option `-p`, if you want to debug a running process:

> 你可以将进程ID作为第二个参数指定，或者使用选项`-p`，如果你想调试一个正在运行的进程：

::: smallexample

```bash
gdb program 1234
gdb -p 1234
```

:::

would attach [GDB] filename.


Taking advantage of the second command-line argument requires a fairly complete operating system; when you use [GDB] will warn you if it is unable to attach or to read core dumps.

> 利用第二个命令行参数需要一个完整的操作系统；当你使用GDB时，它会警告你如果无法附加或读取内存转储。


You can optionally have `gdb` pass any arguments after the executable file to the inferior using `--args`. This option stops option processing.

> 你可以选择使用`--args`让`gdb`将可执行文件后面的任何参数传递给下级。此选项会停止选项处理。

::: smallexample

```bash
gdb --args gcc -O2 -c foo.c
```

:::


This will cause `gdb` to debug `gcc`, and to set `gcc`'s command-line arguments (see [Arguments](Arguments.html#Arguments)) to '`-O2 -c foo.c`'.

> 这会导致`gdb`调试`gcc`，并将`gcc`的命令行参数（参见[参数](Arguments.html#Arguments)）设置为'`-O2 -c foo.c`'。


You can run `gdb` without printing the front material, which describes [GDB]'s non-warranty, by specifying `--silent` (or `-q`/`--quiet`):

> 你可以通过指定`--silent`（或`-q`/`--quiet`）来运行`gdb`而不会打印描述[GDB]非保修情况的前提材料。

::: smallexample

```bash
gdb --silent
```

:::


You can further control how [GDB] itself can remind you of the options available.

> 你可以进一步控制GDB如何提醒你有哪些选项可供选择。

Type

::: smallexample

```bash
gdb -help
```

:::


to display all available options and briefly describe their use ('`gdb -h`' is a shorter equivalent).

> 显示所有可用选项，并简要描述它们的用途（'gdb -h'是一个更短的等效命令）。


All options and command line arguments you give are processed in sequential order. The order makes a difference when the '`-x`' option is used.

> 所有选项和命令行参数按顺序处理。当使用“-x”选项时，顺序会有所不同。

---


• [File Options](File-Options.html#File-Options):                                Choosing files

> • [文件选项](File-Options.html#File-Options):                                选择文件

• [Mode Options](Mode-Options.html#Mode-Options):                                Choosing modes

> • [模式选项](Mode-Options.html#Mode-Options)：选择模式
• [Startup](Startup.html#Startup) does during startup

• [Initialization Files](Initialization-Files.html#Initialization-Files):        Initialization Files

> •[初始化文件](Initialization-Files.html#Initialization-Files):    初始化文件

---

---

::: header
Next: [Quitting GDB](Quitting-GDB.html#Quitting-GDB)]
:::
