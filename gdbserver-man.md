---
tip: translate by openai@2023-06-23 21:38:34
...
---
description: gdbserver man (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: gdbserver man (Debugging with GDB)
lang: en
resource-type: document
title: gdbserver man (Debugging with GDB)
---
::: header
Next: [gcore man](gcore-man.html#gcore-man)]
:::

---

#### gdbserver man

### gdbserver man

::: format

```format
gdbserver comm prog [args…]

gdbserver –attach comm pid

gdbserver –multi comm
```

:::

`gdbserver` is a program that allows you to run [GDB] on a different machine than the one which is running the program being debugged.

#### Usage (server (target) side)


First, you need to have a copy of the program you want to debug put onto the target system. The program can be stripped to save space if needed, as `gdbserver` doesn't care about symbols. All symbol handling is taken care of by the [GDB] running on the host system.

> 首先，您需要将要调试的程序的副本放到目标系统上。如果需要，可以对程序进行剥离以节省空间，因为`gdbserver`不关心符号。主机系统上运行的[GDB]负责所有符号处理。


To use the server, you log on to the target system, and run the `gdbserver` program. You must tell it (a) how to communicate with [GDB], (b) the name of your program, and (c) its arguments. The general syntax is:

> 要使用服务器，您需要登录到目标系统，并运行`gdbserver`程序。您必须告诉它（a）如何与[GDB]进行通信，（b）您的程序的名称以及（c）它的参数。通用语法是：

::: smallexample

```bash
target> gdbserver comm program [args ...]
```

:::

For example, using a serial port, you might say:

::: smallexample

```bash
target> gdbserver /dev/com1 emacs foo.txt
```

:::


This tells `gdbserver` to debug emacs with an argument of foo.txt, and to communicate with [GDB] to communicate with it.

> 这告诉`gdbserver`用foo.txt作为参数来调试emacs，并且与[GDB]进行通信。

To use a TCP connection, you could say:

::: smallexample

```bash
target> gdbserver host:2345 emacs foo.txt
```

:::


This says pretty much the same thing as the last example, except that we are going to communicate with the `host` [GDB]s `target remote` command, which will be described shortly. Note that if you chose a port number that conflicts with another service, `gdbserver` will print an error message and exit.

> 这和上一个例子说的差不多，只是我们要用`host` [GDB] 的`target remote` 命令来通信，稍后会有详细介绍。注意，如果你选择的端口号和其他服务冲突，`gdbserver` 会打印错误信息并退出。

`gdbserver` can also attach to running programs. This is accomplished via the `--attach` argument. The syntax is:

::: smallexample

```bash
target> gdbserver --attach comm pid
```

:::

`pid` is the process ID of a currently running process. It isn't necessary to point `gdbserver` at a binary for the running process.


To start `gdbserver` without supplying an initial command to run or process ID to attach, use the `--multi` to start the program you want to debug.

> 要启动`gdbserver`而不提供要运行的初始命令或要附加的进程ID，请使用`--multi`来启动要调试的程序。

::: smallexample

```bash
target> gdbserver --multi comm
```

:::

#### Usage (host side)


You need an unstripped copy of the target program on your host system, since [GDB]), or a `HOST:PORT` descriptor. For example:

> 您需要在主机系统上有一个未经剥离的目标程序副本，因为[GDB]）或`HOST:PORT`描述符。例如：

::: smallexample

```bash
(gdb) target remote /dev/ttyb
```

:::

communicates with the server via serial line `/dev/ttyb`, and:

::: smallexample

```bash
(gdb) target remote the-target:2345
```

:::


communicates via a TCP connection to port 2345 on host 'the-target', where you previously started up `gdbserver` with the same port number. Note that for TCP connections, you must start up `gdbserver` prior to using the 'target remote' command, otherwise you may get an error that looks something like 'Connection refused'.

> 通过TCP连接到主机“the-target”的端口2345，您之前在该端口号上启动了“gdbserver”。请注意，对于TCP连接，您必须在使用“target remote”命令之前启动“gdbserver”，否则您可能会得到一个类似“连接被拒绝”的错误。

`gdbserver` can also debug multiple inferiors at once, described in [Inferiors Connections and Programs](Inferiors-Connections-and-Programs.html#Inferiors-Connections-and-Programs). In such case use the `extended-remote` [GDB] command variant:

::: smallexample

```bash
(gdb) target extended-remote the-target:2345
```

:::

The `gdbserver` option `--multi` may or may not be used in such case.

There are three different modes for invoking `gdbserver`:

- Debug a specific program specified by its program name:

  ::: smallexample

  ```bash
  gdbserver comm prog [args…]
  ```

  :::

  The `comm` will close the connection, and `gdbserver` will exit.
- Debug a specific program by specifying the process ID of a running program:

  ::: smallexample

  ```bash
  gdbserver --attach comm pid
  ```

  :::

  The `comm` will close the connection, and `gdbserver` will exit.
- Multi-process mode -- debug more than one program/process:

  ::: smallexample

  ```bash
  gdbserver --multi comm
  ```

  :::


  In this mode, [GDB] will not close the connection when a process being debugged exits, so you can debug several processes in the same session.

> 在这种模式下，[GDB]不会在被调试的进程退出时关闭连接，因此您可以在同一个会话中调试多个进程。

In each of the modes you may specify these options:

`--help`

:   List all options, with brief explanations.

`--version`

:   This option causes `gdbserver` to print its version number and exit.

`--attach`

:   `gdbserver` will attach to a running program. The syntax is:

```
::: smallexample
``` smallexample
target> gdbserver --attach comm pid
```

:::

`pid` is the process ID of a currently running process. It isn't necessary to point `gdbserver` at a binary for the running process.

```

`--multi`


:   To start `gdbserver` without supplying an initial command to run or process ID to attach, use this command line option. Then you can connect using [target extended-remote] and start the program you want to debug. The syntax is:

> 要启动`gdbserver`而不提供要运行的初始命令或要附加的进程ID，请使用此命令行选项。然后，您可以使用[target extended-remote]连接并启动要调试的程序。语法是：

```

::: smallexample

```bash
target> gdbserver --multi comm
```

:::

```

`--debug`


:   Instruct `gdbserver` to display extra status information about the debugging process. This option is intended for `gdbserver` development and for bug reports to the developers.

> 请求`gdbserver`显示关于调试过程的额外状态信息。此选项旨在用于`gdbserver`开发和向开发人员提交错误报告。

`--remote-debug`


:   Instruct `gdbserver` to display remote protocol debug output. This option is intended for `gdbserver` development and for bug reports to the developers.

> 请求`gdbserver`显示远程协议调试输出。此选项旨在用于`gdbserver`的开发和向开发人员提交错误报告。

`--debug-file=filename`


:   Instruct `gdbserver` to send any debug output to the given `filename`. This option is intended for `gdbserver` development and for bug reports to the developers.

> 请求`gdbserver`将所有调试输出发送到给定的`文件名`。此选项旨在用于`gdbserver`的开发和向开发人员报告错误。

`--debug-format=option1[,option2,...]`


:   Instruct `gdbserver` to include extra information in each line of debugging output. See [Other Command-Line Arguments for gdbserver](Server.html#Other-Command_002dLine-Arguments-for-gdbserver).

> 请参见[关于gdbserver的其他命令行参数](Server.html#Other-Command_002dLine-Arguments-for-gdbserver)，指示gdbserver在每行调试输出中包含额外信息。

`--wrapper`


:   Specify a wrapper to launch programs for debugging. The option should be followed by the name of the wrapper, then any command-line arguments to pass to the wrapper, then [\--] indicating the end of the wrapper arguments.

> 指定一个包装器来启动用于调试的程序。该选项应该跟随包装器的名称，然后传递给包装器的任何命令行参数，然后[\--]表示包装器参数的结束。

`--once`


:   By default, `gdbserver` keeps the listening TCP port open, so that additional connections are possible. However, if you start `gdbserver` with the `--once` session.

> 默认情况下，`gdbserver` 保持侦听的TCP端口处于打开状态，因此可以进行其他连接。但是，如果您使用`--once`会话启动`gdbserver`，则会关闭侦听的TCP端口。

---

::: header
Next: [gcore man](gcore-man.html#gcore-man)]
:::
```
