---
tip: translate by openai@2023-06-23 12:15:38
...
---
description: gdb man (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: gdb man (Debugging with GDB)
lang: en
resource-type: document
title: gdb man (Debugging with GDB)
---
::: header
Next: [gdbserver man](gdbserver-man.html#gdbserver-man)]
:::

---

#### gdb man

### gdb man


gdb \[OPTIONS] \[`prog`]

> gdb [选项] [prog]


The purpose of a debugger such as [GDB] is to allow you to see what is going on "inside" another program while it executes -- or what another program was doing at the moment it crashed.

> 调试器（比如GDB）的目的是让你在另一个程序执行时能看到它的“内部”情况 —— 或者是另一个程序崩溃时正在做什么。


[GDB] can do four main kinds of things (plus other things in support of these) to help you catch bugs in the act:

> [GDB] 可以做四种主要的事情（以及其他支持这些的事情）来帮助你抓住缺陷：

- Start your program, specifying anything that might affect its behavior.
- Make your program stop on specified conditions.
- Examine what has happened, when your program has stopped.

- Change things in your program, so you can experiment with correcting the effects of one bug and go on to learn about another.

> 更改你的程序中的内容，这样你就可以尝试纠正一个 bug 的影响，并继续学习另一个 bug。


You can use [GDB] to debug programs written in C, C++, Fortran and Modula-2.

> 你可以使用GDB来调试用C、C++、Fortran和Modula-2编写的程序。


[GDB] itself by using the command `help`.

> 使用命令“help”来查看GDB本身的帮助信息。


You can run `gdb` with no arguments or options; but the most usual way to start [GDB] is with one argument or two, specifying an executable program as the argument:

> 你可以不带参数或选项运行`gdb`; 但最常见的启动[GDB]的方式是带一个或两个参数，将可执行程序作为参数。

::: smallexample

```bash
gdb program
```

:::


You can also start with both an executable program and a core file specified:

> 你也可以同时指定可执行程序和内核文件：

::: smallexample

```bash
gdb program core
```

:::


You can, instead, specify a process ID as a second argument or use option `-p`, if you want to debug a running process:

> 你可以用第二个参数指定一个进程ID，或者使用 `-p` 选项，如果你想调试一个正在运行的进程：

::: smallexample

```bash
gdb program 1234
gdb -p 1234
```

:::


would attach [GDB] filename.

> 將[GDB]檔案名稱附加。


Here are some of the most frequently needed [GDB] commands:

> 以下是最常用的GDB命令：

`break [file:][function|line]`


:   Set a breakpoint at `function`).

> 设置一个断点在函数处。

`run [arglist]`


:   Start your program (with `arglist`, if specified).

> 开始你的程序（如果指定，带有`arglist`）。

`bt`


:   Backtrace: display the program stack.

> 回溯：显示程序堆栈。

`print expr`


:   Display the value of an expression.

> 顯示表達式的值。

`c`


:   Continue running your program (after stopping, e.g. at a breakpoint).

> 继续运行您的程序（在停止后，例如在断点处）。

`next`


:   Execute next program line (after stopping); step *over* any function calls in the line.

> 执行下一行程序（停止后）；跳过该行中的任何函数调用。

`edit [file:]function`


:   look at the program line where it is presently stopped.

> 看一下程序当前停止的那一行。

`list [file:]function`


:   type the text of the program in the vicinity of where it is presently stopped.

> 在目前停止的位置附近输入程序文本。

`step`


:   Execute next program line (after stopping); step *into* any function calls in the line.

> 执行下一行程序（停止后）；步入行中的任何函数调用。

`help [name]`


:   Show information about [GDB].

> 显示有关GDB的信息。

`quit`
`exit`

:   Exit from [GDB].


Any arguments other than options specify an executable file and core file (or process ID); that is, the first argument encountered with no associated option flag is equivalent to a `--se` option if it's the name of a file. Many options have both long and abbreviated forms; both are shown here. The long forms are also recognized if you truncate them, so long as enough of the option is present to be unambiguous.

> 除了选项以外的任何参数都指定一个可执行文件和核心文件（或进程ID）；也就是说，如果第一个遇到的没有关联选项标志的参数是文件名，则等同于`--se`选项。许多选项都有长期和缩写形式；这里都显示出来。只要选项足够清晰，也可以识别长期形式的截断。


The abbreviated forms are shown here with '`-` recognizes all of the following conventions for most options:

> 这里显示的缩写形式以 '-’ 识别大多数选项的所有约定：

`--option=value`

`--option value`

`-option=value`

`-option value`

`--o=value`

`--o value`

`-o=value`

`-o value`


All the options and command line arguments you give are processed in sequential order. The order makes a difference when the `-x` option is used.

> 所有给定的选项和命令行参数都按顺序处理。当使用`-x`选项时，顺序就很重要了。

`--help`
`-h`


:   List all options, with brief explanations.

> 列出所有选项，并简要解释。

`--symbols=file`
`-s file`


:   Read symbol table from `file`.

> 从文件中读取符号表。

`--write`


:   Enable writing into executable and core files.

> 启用写入可执行文件和核心文件。

`--exec=file`
`-e file`


:   Use `file` as the executable file to execute when appropriate, and for examining pure data in conjunction with a core dump.

> 使用`文件`作为适当时执行的可执行文件，并且用来与核心转储一起检查纯数据。

`--se=file`


:   Read symbol table from `file` and use it as the executable file.

> 从`文件`中读取符号表，并将其用作可执行文件。

`--core=file`
`-c file`


:   Use `file` as a core dump to examine.

> 使用`文件`作为核心转储来进行检查。

`--command=file`
`-x file`

:   Execute [GDB].

`--eval-command=command`
`-ex command`


:   Execute given [GDB].

> 执行给定的[GDB]。

`--init-eval-command=command`
`-iex`


:   Execute [GDB] before loading the inferior.

> 在加载下属之前执行[GDB]。

`--directory=directory`
`-d directory`


:   Add `directory` to the path to search for source files.

> 将`directory`添加到路径中以搜索源文件。

`--nh`


:   Do not execute commands from `~/.config/gdb/gdbinit`

> 不要从`~/.config/gdb/gdbinit`执行命令。

`--nx`
`-n`


:   Do not execute commands from any `.gdbinit` initialization files.

> 不要执行任何`.gdbinit`初始化文件中的命令。

`--quiet`
`--silent`
`-q`


:   "Quiet". Do not print the introductory and copyright messages. These messages are also suppressed in batch mode.

> 安静。不要打印介绍和版权信息。在批处理模式下也会禁止这些信息。

`--batch`


:   Run in batch mode. Exit with status `0` after processing all the command files specified with `-x` commands in the command files.

> 以批处理模式运行。在处理完命令文件中指定的`-x`命令后，以状态`0`退出。

```
Batch mode may be useful for running [GDB] as a filter, for example to download and run a program on another computer; in order to make this more useful, the message

::: smallexample
``` smallexample

Program exited normally.

> 程序正常退出。
```

:::

(which is ordinarily issued whenever a program running under [GDB] control terminates) is not issued when running in batch mode.

```

`--batch-silent`


:   Run in batch mode, just like `--batch` and would be useless for an interactive session.

> 运行批处理模式，就像`--batch`一样，对于交互式会话没有用处。

```

This is particularly useful when using targets that give '`Loading section`' messages, for example.

Note that targets that give their output via [GDB], as opposed to writing directly to `stdout`, will also be made silent.

```

`--args prog [arglist]`


:   Change interpretation of command line so that arguments following this option are passed as arguments to the inferior. As an example, take the following command:

> 改变命令行的解释，使得后面的参数作为参数传递给次级程序。例如，考虑下面的命令：

```

::: smallexample

```bash
gdb ./a.out -q
```

:::

It would start [GDB], not printing the introductory message. On the other hand, using:

::: smallexample

```bash
gdb --args ./a.out -q
```

:::

starts [GDB] with the introductory message, and passes the option to the inferior.

```

`--pid=pid`

:   Attach [GDB].

`--tui`


:   Open the terminal user interface.

> 打开终端用户界面。

`--readnow`


:   Read all symbols from the given symfile on the first access.

> 从给定的symfile中在第一次访问时读取所有符号。

`--readnever`


:   Do not read symbol files.

> 不要阅读符号文件。

`--return-child-result`


:   [GDB]'s exit code will be the same as the child's exit code.

> GDB的退出代码与子进程的退出代码相同。

`--configuration`


:   Print details about GDB configuration and then exit.

> 打印有关GDB配置的详细信息，然后退出。

`--version`


:   Print version information and then exit.

> 打印版本信息然后退出。

`--cd=directory`


:   Run [GDB] as its working directory, instead of the current directory.

> 运行GDB作为其工作目录，而不是当前目录。

`--data-directory=directory`
`-D`


:   Run [GDB] searches for its auxiliary files.

> 运行GDB搜索其辅助文件。

`--fullname`
`-f`


:   Emacs sets this option when it runs [GDB]' characters as a signal to display the source code for the frame.

> Emacs 在运行 GDB 时会设置这个选项，作为一个信号来显示当前帧的源代码。

`-b baudrate`


:   Set the line speed (baud rate or bits per second) of any serial interface used by [GDB] for remote debugging.

> 设置[GDB]用于远程调试的任何串行接口的线速（波特率或比特每秒）。

`-l timeout`


:   Set timeout, in seconds, for remote debugging.

> 设置远程调试的超时时间（以秒为单位）。

`--tty=device`


:   Run using `device` for your program's standard input and output.

> 使用设备来作为你程序的标准输入和输出。

---

::: header
Next: [gdbserver man](gdbserver-man.html#gdbserver-man)]
:::
```
