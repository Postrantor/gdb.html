---
tip: translate by openai@2023-06-23 19:32:21
...
---
description: Connecting (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Connecting (Debugging with GDB)
lang: en
resource-type: document
title: Connecting (Debugging with GDB)
---
::: header
Next: [File Transfer](File-Transfer.html#File-Transfer)]
:::

---

### 20.1 Connecting to a Remote Target


This section describes how to connect to a remote target, including the types of connections and their differences, how to set up executable and symbol files on the host and target, and the commands used for connecting to and disconnecting from the remote target.

> 本节描述如何连接到远程目标，包括连接类型及其差异、如何在主机和目标上设置可执行文件和符号文件，以及用于连接和断开远程目标的命令。

#### 20.1.1 Types of Remote Connections


[GDB] supports two types of remote connections, `target remote` mode and `target extended-remote` mode. Note that many remote targets support only `target remote` mode. There are several major differences between the two types of connections, enumerated here:

> GDB支持两种远程连接模式，`target remote`模式和`target extended-remote`模式。请注意，许多远程目标只支持`target remote`模式。这两种连接模式之间存在以下几个主要差异：

Result of detach or program exit


**With target remote mode:** When the debugged program exits or you detach from it, [GDB] disconnects from the target. When using `gdbserver`, `gdbserver` will exit.

> 在目标远程模式下：当被调试的程序退出或者你从中分离时，GDB会断开与目标的连接。当使用gdbserver时，gdbserver会退出。


**With target extended-remote mode:** When the debugged program exits or you detach from it, [GDB] remains connected to the target, even though no program is running. You can rerun the program, attach to a running program, or use `monitor` commands specific to the target.

> 在扩展远程模式下：当调试的程序退出或者你从它中分离时，GDB仍然与目标保持连接，即使没有程序在运行。你可以重新运行程序，附加到正在运行的程序，或者使用特定于目标的`monitor`命令。


When using `gdbserver` in this case, it does not exit unless it was invoked using the `--once` option was not used, you can ask `gdbserver` to exit using the `monitor exit` command (see [Monitor Commands for gdbserver](Server.html#Monitor-Commands-for-gdbserver)).

> 当在这种情况下使用`gdbserver`时，除非使用`--once`选项调用，否则它不会退出，您可以使用`monitor exit`命令要求`gdbserver`退出（请参阅[gdbserver的监视器命令]（Server.html#Monitor-Commands-for-gdbserver））。

Specifying the program to debug


For both connection types you use the `file` command to specify the program on the host system. If you are using `gdbserver` there are some differences in how to specify the location of the program on the target.

> 对于两种连接类型，您都可以使用`file`命令来指定主机系统上的程序。如果您正在使用`gdbserver`，则指定目标上程序的位置有一些不同。


**With target remote mode:** You must either specify the program to debug on the `gdbserver` command line or use the `--attach` option (see [Attaching to a Running Program](Server.html#Attaching-to-a-program)).

> 在目标远程模式下：您必须在`gdbserver`命令行中指定要调试的程序，或者使用`--attach`选项（请参阅[附加到正在运行的程序](Server.html#Attaching-to-a-program)）。


**With target extended-remote mode:** You may specify the program to debug on the `gdbserver` command line, or you can load the program or attach to it using [GDB] commands after connecting to `gdbserver`.

> 在扩展远程模式下：您可以在`gdbserver`命令行中指定要调试的程序，也可以在连接到`gdbserver`后使用[GDB]命令加载程序或附加到它。


You can start `gdbserver` without supplying an initial command to run or process ID to attach. To do this, use the `--multi` option to `gdbserver` has no influence on that.

> 你可以在不提供要运行的初始命令或要附加的进程ID的情况下启动`gdbserver`。要做到这一点，请使用`gdbserver`的`--multi`选项，这对此没有影响。

The `run` command


**With target remote mode:** The `run` command is not supported. Once a connection has been established, you can use all the usual [GDB].

> 在目标远程模式下：不支持`run`命令。一旦建立连接，您可以使用所有常见的[GDB]命令。


**With target extended-remote mode:** The `run` command is supported. The `run` command uses the value set by `set remote exec-file` (see [set remote exec-file](Remote-Configuration.html#set-remote-exec_002dfile)) to select the program to run. Command line arguments are supported, except for wildcard expansion and I/O redirection (see [Arguments](Arguments.html#Arguments)).

> 在延伸遠程模式下：支持 `run` 命令。 `run` 命令使用 `set remote exec-file` 設置的值（詳見[設置遠程執行文件](Remote-Configuration.html#set-remote-exec_002dfile)) 來選擇要運行的程序。支持命令行參數，但不支持通配符展開和 I/O 重定向（詳見[參數](Arguments.html#Arguments))。


If you specify the program to debug on the command line, then the `run` command is not required to start execution, and you can resume using commands like [step] as with `target remote` mode.

> 如果在命令行中指定要调试的程序，则不需要使用`run`命令来启动执行，而且您可以使用像[step]这样的命令继续执行，就像`target remote`模式一样。

Attaching


**With target remote mode:** The [GDB] option (see [Running gdbserver](Server.html#Running-gdbserver)).

> **使用目标远程模式：**[GDB] 选项（参见[运行 gdbserver](Server.html#Running-gdbserver)）。


**With target extended-remote mode:** To attach to a running program, you may use the `attach` command after the connection has been established. If you are using `gdbserver`, you may also invoke `gdbserver` using the `--attach` option (see [Running gdbserver](Server.html#Running-gdbserver)).

> 在扩展远程模式下：要连接到正在运行的程序，在建立连接后，可以使用`attach`命令。如果使用`gdbserver`，也可以使用`--attach`选项调用`gdbserver`（参见[运行 gdbserver](Server.html#Running-gdbserver)）。


Some remote targets allow [GDB] (see [set exec-file-mismatch](Attach.html#set-exec_002dfile_002dmismatch)).

> 一些远程目标允许使用[GDB](参见[设置exec-file-mismatch](Attach.html#set-exec_002dfile_002dmismatch))。

#### 20.1.2 Host and Target Files


[GDB], running on the host, needs access to symbol and debugging information for your program running on the target. This requires access to an unstripped copy of your program, and possibly any associated symbol files. Note that this section applies equally to both `target remote` mode and `target extended-remote` mode.

> [GDB] 在主机上运行，需要访问正在目标上运行的程序的符号和调试信息。这需要访问一个未剥离的程序副本，以及可能的任何相关符号文件。请注意，本节同样适用于“target remote”模式和“target extended-remote”模式。


Some remote targets (see [qXfer executable filename read](General-Query-Packets.html#qXfer-executable-filename-read), and see [Host I/O Packets](Host-I_002fO-Packets.html#Host-I_002fO-Packets)) allow [GDB]. With such a target, if the remote program is unstripped, the only command you need is `target remote` (or `target extended-remote`).

> 一些远程目标（参见[qXfer可执行文件名称读取](General-Query-Packets.html#qXfer-executable-filename-read)，并参见[主机I/O数据包](Host-I_002fO-Packets.html#Host-I_002fO-Packets)）允许[GDB]。对于这样的目标，如果远程程序未被剥离，则唯一需要的命令是`target remote`（或`target extended-remote`）。


If the remote program is stripped, or the target does not support remote program file access, start up [GDB] locates target libraries.

> 如果远程程序被剥离，或者目标不支持远程程序文件访问，可以启动[GDB]定位目标库。


The symbol file and target libraries must exactly match the executable and libraries on the target, with one exception: the files on the host system should not be stripped, even if the files on the target system are. Mismatched or missing files will lead to confusing results during debugging. On [GNU]/Linux targets, mismatched or missing files may also prevent `gdbserver` from debugging multi-threaded programs.

> 符号文件和目标库必须与目标上的可执行文件和库完全匹配，唯一的例外是：主机系统上的文件不应该被剥离，即使目标系统上的文件被剥离了也不行。不匹配或缺失的文件会导致调试时出现令人困惑的结果。在[GNU]/Linux目标上，不匹配或缺失的文件也可能会阻止`gdbserver`调试多线程程序。

#### 20.1.3 Remote Connection Commands


[GDB] uses the same protocol for debugging your program; only the medium carrying the debugging packets varies. The `target remote` and `target extended-remote` commands establish a connection to the target. Both commands accept the same arguments, which indicate the medium to use:

> GDB使用相同的协议来调试您的程序；只有携带调试数据包的媒介不同。`target remote`和`target extended-remote`命令建立到目标的连接。这两个命令接受相同的参数，指示要使用的媒介：

`target remote serial-device`
`target extended-remote serial-device`

:

```
Use `serial-device`:

::: smallexample
``` smallexample
target remote /dev/ttyb
```

:::

If you're using a serial line, you may want to give [GDB]' option, or use the `set serial baud` command (see [set serial baud](Remote-Configuration.html#Remote-Configuration)) before the `target` command.

```

`target remote local-socket`
`target extended-remote local-socket`

:   

```

Use `local-socket`:

::: smallexample

```bash
target remote /tmp/gdb-socket0
```

:::

Note that this command has the same form as the command to connect to a serial line. [GDB] will automatically determine which kind of file you have specified and will make the appropriate kind of connection. This feature is not available if the host system does not support Unix domain sockets.

```

`target remote host:port`
`target remote [host]:port`
`target remote tcp:host:port`
`target remote tcp:[host]:port`
`target remote tcp4:host:port`
`target remote tcp6:host:port`
`target remote tcp6:[host]:port`
`target extended-remote host:port`
`target extended-remote [host]:port`
`target extended-remote tcp:host:port`
`target extended-remote tcp:[host]:port`
`target extended-remote tcp4:host:port`
`target extended-remote tcp6:host:port`
`target extended-remote tcp6:[host]:port`

:   

```

Debug using a TCP connection to `port` could be the target machine itself, if it is directly connected to the net, or it might be a terminal server which in turn has a serial line to the target.

For example, to connect to port 2828 on a terminal server named `manyfarms`:

::: smallexample

```bash
target remote manyfarms:2828
```

:::

To connect to port 2828 on a terminal server whose address is `2001:0db8:85a3:0000:0000:8a2e:0370:7334`, you can either use the square bracket syntax:

::: smallexample

```bash
target remote [2001:0db8:85a3:0000:0000:8a2e:0370:7334]:2828
```

:::

or explicitly specify the IPv6 protocol:

::: smallexample

```bash
target remote tcp6:2001:0db8:85a3:0000:0000:8a2e:0370:7334:2828
```

:::

This last example may be confusing to the reader, because there is no visible separation between the hostname and the port number. Therefore, we recommend the user to provide IPv6 addresses using square brackets for clarity. However, it is important to mention that for [GDB] there is no ambiguity: the number after the last colon is considered to be the port number.

If your remote target is actually running on the same machine as your debugger session (e.g. a simulator for your target running on the same host), you can omit the hostname. For example, to connect to port 1234 on your local machine:

::: smallexample

```bash
target remote :1234
```

:::

Note that the colon is still required here.

```

`target remote udp:host:port`
`target remote udp:[host]:port`
`target remote udp4:host:port`
`target remote udp6:[host]:port`
`target extended-remote udp:host:port`
`target extended-remote udp:host:port`
`target extended-remote udp:[host]:port`
`target extended-remote udp4:host:port`
`target extended-remote udp6:host:port`
`target extended-remote udp6:[host]:port`

:   

```

Debug using UDP packets to `port`. For example, to connect to UDP port 2828 on a terminal server named `manyfarms`:

::: smallexample

```bash
target remote udp:manyfarms:2828
```

:::

When using a UDP connection for remote debugging, you should keep in mind that the 'U' stands for "Unreliable". UDP can silently drop packets on busy or unreliable networks, which will cause havoc with your debugging session.

```

`target remote | command`
`target extended-remote | command`

:   

```

Run `command` is a shell command, to be parsed and expanded by the system's command shell, `/bin/sh`; it should expect remote protocol packets on its standard input, and send replies on its standard output. You could use this to run a stand-alone simulator that speaks the remote debugging protocol, to make net connections using programs like `ssh`, or for other similar tricks.

If `command` will try to send it a `SIGTERM` signal. (If the program has already exited, this will have no effect.)

```



Whenever [GDB] displays this prompt:

::: smallexample

```bash
Interrupted while waiting for the program.
Give up (and stop debugging it)?  (y or n)
```

:::

In `target remote` mode, if you type [y] goes back to waiting.

In `target extended-remote` mode, typing [n] connected to the target.

`detach`


When you have finished debugging the remote program, you can use the `detach` command to release it from [GDB] is still connected to the target.

> 当您完成调试远程程序后，您可以使用`detach`命令将其从[GDB]断开连接，仍然连接到目标。

`disconnect`


The `disconnect` command closes the connection to the target, and the target is generally not resumed. It will wait for [GDB] is again free to connect to another target.

> 命令`断开`关闭与目标的连接，通常不会恢复目标。它将等待[GDB]再次可以连接到另一个目标。

`monitor cmd`


This command allows you to send arbitrary commands directly to the remote monitor. Since [GDB]---you can add new commands that only the external monitor will understand and implement.

> 这个命令允许你直接向远程监视器发送任意命令。自从[GDB]以来，你可以添加只有外部监视器才能理解和实现的新命令。

---

::: header
Next: [File Transfer](File-Transfer.html#File-Transfer)]
:::
