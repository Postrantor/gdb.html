---
tip: translate by openai@2023-06-24 02:31:02
...
---
description: Server (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Server (Debugging with GDB)
lang: en
resource-type: document
title: Server (Debugging with GDB)
---
::: header
Next: [Remote Configuration](Remote-Configuration.html#Remote-Configuration)]
:::

---

### 20.3 Using the `gdbserver` Program

`gdbserver` is a control program for Unix-like systems, which allows you to connect your program with a remote [GDB] via `target remote` or `target extended-remote`---but without linking in the usual debugging stub.

`gdbserver` is not a complete replacement for the debugging stubs, because it requires essentially the same operating-system facilities that [GDB], so you may be able to get started more quickly on a new system by using `gdbserver`. Finally, if you develop code for real-time systems, you may find that the tradeoffs involved in real-time operation make it more convenient to do as much development work as possible on another system, for example by cross-compiling. You can use `gdbserver` to make a similar choice for debugging.

[GDB] remote serial protocol.

> *Warning:* `gdbserver` does not have any built-in security. Do not run `gdbserver` connected to any public network; a [GDB] connection to `gdbserver` provides access to the target system with the same privileges as the user running `gdbserver`.

#### 20.3.1 Running `gdbserver`


Run `gdbserver` on the target system. You need a copy of the program you want to debug, including any libraries it requires. `gdbserver` does not need your program's symbol table, so you can strip the program if necessary to save space. [GDB] on the host system does all the symbol handling.

> 在目标系统上运行`gdbserver`。您需要要调试的程序的副本，包括它所需的任何库。`gdbserver`不需要您的程序的符号表，因此您可以在必要时剥离程序以节省空间。[GDB]在主机系统上处理所有符号。


To use the server, you must tell it how to communicate with [GDB]; the name of your program; and the arguments for your program. The usual syntax is:

> 要使用服务器，您必须告诉它如何与GDB进行通信；您程序的名称；以及您程序的参数。通常的语法是：

::: smallexample

```bash
target> gdbserver comm program [ args … ]
```

:::

`comm`:

::: smallexample

```bash
target> gdbserver /dev/com1 emacs foo.txt
```

:::

`gdbserver` waits passively for the host [GDB] to communicate with it.

To use a TCP connection instead of a serial line:

::: smallexample

```bash
target> gdbserver host:2345 emacs foo.txt
```

:::


The only difference from the previous example is the first argument, specifying that you are communicating with the host [GDB] `target remote` command.

> 前一个例子唯一的不同是第一个参数，指定你正在使用`target remote`命令与主机[GDB]进行通信。

The `stdio` connection is useful when starting `gdbserver` with ssh:

::: smallexample

```bash
(gdb) target remote | ssh -T hostname gdbserver - hello
```

:::


The '`-T`' option to ssh is provided because we don't need a remote pty, and we don't want escape-character handling. Ssh does this by default when a command is provided, the flag is provided to make it explicit. You could elide it if you want to.

> ssh提供了'-T'选项，因为我们不需要远程pty，也不需要处理转义字符。当提供命令时，ssh会默认这样做，该标志是为了明确表达。如果你想的话，你可以省略它。


Programs started with stdio-connected gdbserver have `/dev/null` for `stdin`, and `stdout`,`stderr` are sent back to gdb for display through a pipe connected to gdbserver. Both `stdout` and `stderr` use the same pipe.

> 程序通过使用stdio连接的gdbserver启动，stdin使用`/dev/null`，stdout和stderr通过连接到gdbserver的管道发送回gdb来显示，stdout和stderr使用相同的管道。

#### 20.3.1.1 Attaching to a Running Program


On some targets, `gdbserver` can also attach to running programs. This is accomplished via the `--attach` argument. The syntax is:

> 在某些目标上，`gdbserver`也可以附加到正在运行的程序。这是通过`--attach`参数实现的。语法为：

::: smallexample

```bash
target> gdbserver --attach comm pid
```

:::

`pid` is the process ID of a currently running process. It isn't necessary to point `gdbserver` at a binary for the running process.


In `target extended-remote` mode, you can also attach using the [GDB] attach command (see [Attaching in Types of Remote Connections](Connecting.html#Attaching-in-Types-of-Remote-Connections)).

> 在`target extended-remote`模式下，你也可以使用[GDB] attach命令进行附加（参见[在远程连接类型中附加](Connecting.html#Attaching-in-Types-of-Remote-Connections)）。


You can debug processes by name instead of process ID if your target has the `pidof` utility:

> 你可以通过名称而不是进程ID来调试进程，如果你的目标有`pidof`实用程序：

::: smallexample

```bash
target> gdbserver --attach comm `pidof program`
```

:::


In case more than one copy of `program` has multiple threads, most versions of `pidof` support the `-s` option to only return the first process ID.

> 如果程序有多个副本，每个副本都有多个线程，大多数版本的pidof支持-s选项，只返回第一个进程ID。

#### 20.3.1.2 TCP port allocation lifecycle of `gdbserver`


This section applies only when `gdbserver` is run to listen on a TCP port.

> 此部分仅适用于在TCP端口上运行`gdbserver`时。

`gdbserver` normally terminates after all of its debugged processes have terminated in [target remote] mode.

When `gdbserver` stays running, [GDB] can be connected at a time.


By default, `gdbserver` keeps the listening TCP port open, so that subsequent connections are possible. However, if you start `gdbserver` with the `--once` option allows reusing the same port number for connecting to multiple instances of `gdbserver` running on the same host, since each instance closes its port after the first connection.

> 默认情况下，gdbserver保持监听TCP端口处于打开状态，以便允许后续连接。但是，如果使用--once选项启动gdbserver，则可以将相同的端口号用于连接到同一主机上运行的多个gdbserver实例，因为每个实例在第一次连接后都会关闭其端口。

#### 20.3.1.3 Other Command-Line Arguments for `gdbserver`


You can use the `--multi` option to start `gdbserver` without specifying a program to debug or a process to attach to. Then you can attach in `target extended-remote` mode and run or attach to a program. For more information, see [\--multi Option in Types of Remote Connnections](Connecting.html#g_t_002d_002dmulti-Option-in-Types-of-Remote-Connnections).

> 你可以使用`--multi`选项来启动`gdbserver`，而无需指定要调试的程序或要附加的进程。然后，你可以以`target extended-remote`模式连接，并运行或附加到一个程序。有关更多信息，请参见[远程连接类型中的--multi选项](Connecting.html#g_t_002d_002dmulti-Option-in-Types-of-Remote-Connnections)。


The `--debug`. These options are intended for `gdbserver` development and for bug reports to the developers.

> `--debug` 选项旨在用于`gdbserver`开发和向开发者报告错误。


The `--debug-format=option1[,option2,...]` option tells `gdbserver` to include additional information in each output. Possible options are:

> `--debug-format=option1[,option2,...]` 选项告诉`gdbserver`在每次输出中包含额外的信息。可能的选项有：

`none`

:   Turn off all extra information in debugging output.

`all`

:   Turn on all extra information in debugging output.

`timestamps`

:   Include a timestamp in each line of debugging output.


Options are processed in order. Thus, for example, if `none` appears last then no additional information is added to debugging output.

> 选项按顺序处理。因此，例如，如果`none`出现在最后，则不会向调试输出添加其他信息。

The `--wrapper` indicating the end of the wrapper arguments.

`gdbserver` runs the specified wrapper program with a combined command line including the wrapper arguments, then the name of the program to debug, then any arguments to the program. The wrapper runs until it executes your program, and then [GDB] gains control.


You can use any program that eventually calls `execve` with its arguments as a wrapper. Several standard Unix utilities do this, e.g. `env` and `nohup`. Any Unix shell script ending with `exec "$@"` will also work.

> 你可以使用任何最终调用`execve`并带有它的参数的程序作为一个包装器。几个标准的Unix实用程序都可以做到这一点，例如`env`和`nohup`。任何以`exec“$ @”`结尾的Unix shell脚本也可以工作。


For example, you can use `env` to pass an environment variable to the debugged program, without setting the variable in `gdbserver`'s environment:

> 例如，您可以使用`env`将环境变量传递给调试程序，而无需在`gdbserver`的环境中设置变量：

::: smallexample

```bash
$ gdbserver --wrapper env LD_PRELOAD=libtest.so -- :2222 ./testprog
```

:::

The `--selftest` option runs the self tests in `gdbserver`:

::: smallexample

```bash
$ gdbserver --selftest
Ran 2 unit tests, 0 failed
```

:::

These tests are disabled in release.

#### 20.3.2 Connecting to `gdbserver`

The basic procedure for connecting to the remote target is:

- Run [GDB] on the host system.

- Make sure you have the necessary symbol files (see [Host and target files](Connecting.html#Host-and-target-files)). Load symbols for your application using the `file` command before you connect. Use `set sysroot` to locate target libraries (unless your [GDB] was compiled with the correct sysroot using `--with-sysroot`).

> 确保您有必要的符号文件（参见[主机和目标文件](Connecting.html#Host-and-target-files)）。在连接之前，使用`file`命令加载您的应用程序的符号。使用`set sysroot`定位目标库（除非您的[GDB]使用`--with-sysroot`编译时带有正确的sysroot）。

- Connect to your target (see [Connecting to a Remote Target](Connecting.html#Connecting)). For TCP connections, you must start up `gdbserver` prior to using the `target` command. Otherwise you may get an error whose text depends on the host system, but which usually looks something like '`Connection refused` when using `target remote` mode, since the program is already on the target.

> 连接到你的目标（参见[连接远程目标](Connecting.html#Connecting))。对于TCP连接，在使用`target`命令之前必须启动`gdbserver`。否则，您可能会收到一个错误，其文本取决于主机系统，但通常看起来像‘使用`target remote`模式时的`连接被拒绝`，因为程序已经在目标上。

#### 20.3.3 Monitor Commands for `gdbserver`


During a [GDB] session using `gdbserver`, you can use the `monitor` command to send special requests to `gdbserver`. Here are the available commands.

> 在使用`gdbserver`的GDB会话中，您可以使用`monitor`命令向`gdbserver`发送特殊请求。以下是可用的命令。

`monitor help`

:   List the available monitor commands.

`monitor set debug 0`
`monitor set debug 1`

:   Disable or enable general debugging messages.

`monitor set remote-debug 0`
`monitor set remote-debug 1`


:   Disable or enable specific debugging messages associated with the remote protocol (see [Remote Protocol](Remote-Protocol.html#Remote-Protocol)).

> 禁用或启用与远程协议相关的特定调试消息（参见[远程协议](Remote-Protocol.html#Remote-Protocol)）。

`monitor set debug-file filename`
`monitor set debug-file`

:   Send any debug output to the given file, or to stderr.

`monitor set debug-format option1[,option2,...]`


:   Specify additional text to add to debugging messages. Possible options are:

> 指定要添加到调试消息中的其他文本。可能的选项是：

```
`none`

:   Turn off all extra information in debugging output.

`all`

:   Turn on all extra information in debugging output.

`timestamps`

:   Include a timestamp in each line of debugging output.

Options are processed in order. Thus, for example, if `none` appears last then no additional information is added to debugging output.
```

`monitor set libthread-db-search-path [PATH]`

:

```
When this command is issued, `path`' will be reset to its default value.

The special entry '`$pdir`' is not supported in `gdbserver`.
```

`monitor exit`


:   Tell gdbserver to exit immediately. This command should be followed by `disconnect` to close the debugging session. `gdbserver` will detach from any attached processes and kill any processes it created. Use `monitor exit` to terminate `gdbserver` at the end of a multi-process mode debug session.

> 告诉gdbserver立即退出。此命令应该跟随`断开`以关闭调试会话。`gdbserver`将从任何附加的进程中分离，并杀死它创建的任何进程。使用`monitor exit`在多进程模式调试会话结束时终止`gdbserver`。

#### 20.3.4 Tracepoints support in `gdbserver`


On some targets, `gdbserver` supports tracepoints, fast tracepoints and static tracepoints.

> 在某些目标上，`gdbserver`支持跟踪点、快速跟踪点和静态跟踪点。


For fast or static tracepoints to work, a special library called the *in-process agent* (IPA), must be loaded in the inferior process. This library is built and distributed as an integral part of `gdbserver`. In addition, support for static tracepoints requires building the in-process agent library with static tracepoints support. At present, the UST (LTTng Userspace Tracer, [http://lttng.org/ust](http://lttng.org/ust)) tracing engine is supported. This support is automatically available if UST development headers are found in the standard include path when `gdbserver` is built, or if `gdbserver` was explicitly configured using `--with-ust`.

> 为了使快速或静态跟踪点可以正常工作，必须在次级进程中加载一个特殊的库，称为*进程内代理*（IPA）。该库作为`gdbserver`的一个组成部分构建和分发。此外，支持静态跟踪点需要使用静态跟踪点支持构建进程内代理库。目前，支持UST（LTTng用户空间跟踪器，[http://lttng.org/ust](http://lttng.org/ust)）跟踪引擎。如果在构建`gdbserver`时在标准包含路径中找到UST开发头文件，或者使用`--with-ust`显式配置`gdbserver`，则自动可用。

There are several ways to load the in-process agent in your program:

`Specifying it as dependency at link time`


:   You can link your program dynamically with the in-process agent library. On most systems, this is accomplished by adding `-linproctrace` to the link command.

> 你可以动态地将你的程序与内置进程代理库链接起来。在大多数系统上，可以通过将'-linproctrace'添加到链接命令来实现。

`Using the system's preloading mechanisms`


:   You can force loading the in-process agent at startup time by using your system's support for preloading shared libraries. Many Unixes support the concept of preloading user defined libraries. In most cases, you do that by specifying `LD_PRELOAD=libinproctrace.so` in the environment. See also the description of `gdbserver`'s `--wrapper` command line option.

> 你可以通过使用系统支持的预加载共享库来在启动时强制加载内部进程代理。许多Unix都支持预加载用户定义库的概念。在大多数情况下，你可以通过在环境中指定`LD_PRELOAD=libinproctrace.so`来实现。另外，也可以参考`gdbserver`的`--wrapper`命令行选项的描述。

`Using GDB to force loading the agent at run time`


:   On some systems, you can force the inferior to load a shared library, by calling a dynamic loader function in the inferior that takes care of dynamically looking up and loading a shared library. On most Unix systems, the function is `dlopen`. You'll use the `call` command for that. For example:

> 在某些系统上，您可以通过在次级中调用动态加载程序函数来强制次级加载共享库。在大多数Unix系统上，该函数为“dlopen”。您将使用“call”命令来执行此操作。例如：

```
::: smallexample
``` smallexample
(gdb) call dlopen ("libinproctrace.so", ...)
```

:::

Note that on most Unix systems, for the `dlopen` function to be available, the program needs to be linked with `-ldl`.

```


On systems that have a userspace dynamic loader, like most Unix systems, when you connect to `gdbserver` using `target remote`, you'll find that the program is stopped at the dynamic loader's entry point, and no shared library has been loaded in the program's address space yet, including the in-process agent. In that case, before being able to use any of the fast or static tracepoints features, you need to let the loader run and load the shared libraries. The simplest way to do that is to run the program to the main procedure. E.g., if debugging a C or C++ program, start `gdbserver` like so:

> 在有用户空间动态加载器的系统上，比如大多数Unix系统，当你使用`target remote`连接到`gdbserver`时，你会发现程序已经停止在动态加载器的入口点，而且程序的地址空间中还没有加载任何共享库，包括内部代理。在这种情况下，在能够使用任何快速或静态跟踪点功能之前，你需要让加载器运行并加载共享库。最简单的方法是将程序运行到主程序。例如，如果调试C或C++程序，可以像这样启动`gdbserver`:

::: smallexample

```bash
$ gdbserver :9999 myprogram
```

:::

Start GDB and connect to `gdbserver` like so, and run to main:

::: smallexample

```bash
$ gdb myprogram
(gdb) target remote myhost:9999
0x00007f215893ba60 in ?? () from /lib64/ld-linux-x86-64.so.2
(gdb) b main
(gdb) continue
```

:::


The in-process tracing agent library should now be loaded into the process; you can confirm it with the `info sharedlibrary` command, which will list `libinproctrace.so` as loaded in the process. You are now ready to install fast tracepoints, list static tracepoint markers, probe static tracepoints markers, and start tracing.

> 现在应该将进程跟踪代理库加载到进程中；您可以使用`info sharedlibrary`命令确认它，它将列出`libinproctrace.so`作为进程中加载的内容。您现在可以安装快速跟踪点、列出静态跟踪点标记、探测静态跟踪点标记，并开始跟踪。

::: footnote

---

#### Footnotes

### [(16)](#DOCF16)


If you choose a port number that conflicts with another service, `gdbserver` prints an error message and exits.

> 如果你选择一个与另一个服务冲突的端口号，`gdbserver`会打印出一条错误消息并退出。
:::

---

::: header
Next: [Remote Configuration](Remote-Configuration.html#Remote-Configuration)]
:::
