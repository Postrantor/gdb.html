---
tip: translate by openai@2023-06-23 23:31:22
...
---
description: Input/Output (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Input/Output (Debugging with GDB)
lang: en
resource-type: document
title: Input/Output (Debugging with GDB)
---
::: header
Next: [Attach](Attach.html#Attach)]
:::

---

### 4.6 Your Program's Input and Output


By default, the program you run under [GDB] switches the terminal to its own terminal modes to interact with you, but it records the terminal modes your program was using and switches back to them when you continue running your program.

> 默认情况下，您在[GDB]下运行的程序会切换到自己的终端模式与您交互，但它会记录您的程序使用的终端模式，并在您继续运行程序时切换回它们。

`info terminal`


Displays information recorded by [GDB] about the terminal modes your program is using.

> 显示[GDB]记录的关于您的程序正在使用的终端模式的信息。


You can redirect your program's input and/or output using shell redirection with the `run` command. For example,

> 你可以使用`run`命令通过shell重定向来重定向你程序的输入和/或输出。例如，

::: smallexample

```bash
run > outfile
```

:::

starts your program, diverting its output to the file `outfile`.


Another way to specify where your program should do input and output is with the `tty` command. This command accepts a file name as argument, and causes this file to be the default for future `run` commands. It also resets the controlling terminal for the child process, for future `run` commands. For example,

> 另一种指定程序输入和输出位置的方法是使用`tty`命令。此命令接受文件名作为参数，并使该文件成为未来`run`命令的默认文件。它还会重置子进程的控制终端，以供未来的`run`命令使用。例如，

::: smallexample

```bash
tty /dev/ttyb
```

:::


directs that processes started with subsequent `run` commands default to do input and output on the terminal `/dev/ttyb` and have that as their controlling terminal.

> 命令指定通过后续的`run`命令启动的进程默认使用终端`/dev/ttyb`进行输入和输出，并将其作为其控制终端。


An explicit redirection in `run` overrides the `tty` command's effect on the input/output device, but not its effect on the controlling terminal.

> 运行中的显式重定向会覆盖`tty`命令对输入/输出设备的影响，但不会影响它对控制终端的影响。


When you use the `tty` command or redirect input in the `run` command, only the input *for your program* is affected. The input for [GDB] still comes from your terminal. `tty` is an alias for `set inferior-tty`.

> 当你使用'tty'命令或者在'run'命令中重定向输入时，只有你的程序的输入会受到影响。[GDB]的输入仍然来自你的终端。'tty'是'set inferior-tty'的别名。


You can use the `show inferior-tty` command to tell [GDB] to display the name of the terminal that will be used for future runs of your program.

> 你可以使用`show inferior-tty`命令来告诉GDB显示将来运行程序时使用的终端的名称。

`set inferior-tty [ tty ]`

:

```
Set the tty for the program being debugged to `tty`.
```

`show inferior-tty`

:

```
Show the current tty for the program being debugged.
```

---

::: header
Next: [Attach](Attach.html#Attach)]
:::
