---
tip: translate by openai@2023-06-23 21:13:10
...
---
description: Forks (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Forks (Debugging with GDB)
lang: en
resource-type: document
title: Forks (Debugging with GDB)
---
::: header
Next: [Checkpoint/Restart](Checkpoint_002fRestart.html#Checkpoint_002fRestart)]
:::

---

### 4.11 Debugging Forks


On most systems, [GDB] will continue to debug the parent process and the child process will run unimpeded. If you have set a breakpoint in any code which the child then executes, the child will get a `SIGTRAP` signal which (unless it catches the signal) will cause it to terminate.

> 在大多数系统中，[GDB]将继续调试父进程，子进程将不受阻碍地运行。如果您在子进程执行的任何代码中设置了断点，子进程将收到一个`SIGTRAP`信号（除非它捕获该信号），否则将导致其终止。


However, if you want to debug the child process there is a workaround which isn't too painful. Put a call to `sleep` in the code which the child process executes after the fork. It may be useful to sleep only if a certain environment variable is set, or a certain file exists, so that the delay need not occur when you don't want to run [GDB] if you are also debugging the parent process) to attach to the child process (see [Attach](Attach.html#Attach)). From that point on you can debug the child process just like any other process which you attached to.

> 然而，如果你想要调试子进程，有一个可行的解决方案，它并不太痛苦。在子进程在fork之后执行的代码中添加一个`sleep`调用。如果设置了某个环境变量或者存在某个文件，可以只睡眠，这样就不需要在你不想运行[GDB]时出现延迟，如果你也在调试父进程的话）来附加到子进程（参见[Attach]（Attach.html#Attach））。从那时起，你就可以像调试其他附加进程一样调试子进程。


On some systems, [GDB]/Linux platforms, this feature is supported with kernel version 2.5.46 and later.

> 在某些系统，[GDB]/Linux 平台，这一特性是支持内核版本2.5.46及更高版本的。


The fork debugging commands are supported in native mode and when connected to `gdbserver` in either `target remote` mode or `target extended-remote` mode.

> 命令行调试叉子在本地模式下支持，当连接到`gdbserver`时，可以使用`target remote`模式或`target extended-remote`模式。


By default, when a program forks, [GDB] will continue to debug the parent process and the child process will run unimpeded.

> 默认情况下，当程序分叉时，[GDB]将继续调试父进程，而子进程将不受阻碍地运行。


If you want to follow the child process instead of the parent process, use the command `set follow-fork-mode`.

> 如果你想跟踪子进程而不是父进程，请使用命令“set follow-fork-mode”。

`set follow-fork-mode mode`


Set the debugger response to a program call of `fork` or `vfork`. A call to `fork` or `vfork` creates a new process. The `mode` argument can be:

> 设置调试器对`fork`或`vfork`程序调用的响应。对`fork`或`vfork`的调用会创建一个新的进程。`mode`参数可以是：

`parent`


:   The original process is debugged after a fork. The child process runs unimpeded. This is the default.

> 原始进程在分叉后调试完毕，子进程无阻碍地运行，这是默认情况。

`child`


:   The new process is debugged after a fork. The parent process runs unimpeded.

> 新进程在分叉后被调试，父进程继续无阻碍地运行。

`show follow-fork-mode`

Display the current debugger response to a `fork` or `vfork` call.


On Linux, if you want to debug both the parent and child processes, use the command `set detach-on-fork`.

> 在Linux上，如果你想调试父进程和子进程，请使用命令`set detach-on-fork`。

`set detach-on-fork mode`


Tells gdb whether to detach one of the processes after a fork, or retain debugger control over them both.

> 告诉GDB在fork之后是否要分离其中一个进程，或者保持调试器对它们两个的控制。

`on`


:   The child process (or parent process, depending on the value of `follow-fork-mode`) will be detached and allowed to run independently. This is the default.

> 子进程（或根据`follow-fork-mode`的值而定的父进程）将被分离，允许独立运行。这是默认设置。

`off`


:   Both processes will be held under the control of [GDB]. One process (child or parent, depending on the value of `follow-fork-mode`) is debugged as usual, while the other is held suspended.

> 两个进程都将在GDB的控制下进行。根据follow-fork-mode的值，一个进程（子进程或父进程）将按照常规方式调试，而另一个进程将被挂起。

`show detach-on-fork`

Show whether detach-on-fork mode is on/off.


If you choose to set '`detach-on-fork` by using the `info inferiors` command, and switch from one fork to another by using the `inferior` command (see [Debugging Multiple Inferiors Connections and Programs](Inferiors-Connections-and-Programs.html#Inferiors-Connections-and-Programs)).

> 如果您选择使用`info inferiors`命令设置'detach-on-fork'，并通过使用`inferior`命令从一个分支切换到另一个分支（参见[Debugging Multiple Inferiors Connections and Programs](Inferiors-Connections-and-Programs.html#Inferiors-Connections-and-Programs))，


To quit debugging one of the forked processes, you can either detach from it by using the `detach inferiors` command (allowing it to run independently), or kill it using the `kill inferiors` command. See [Debugging Multiple Inferiors Connections and Programs](Inferiors-Connections-and-Programs.html#Inferiors-Connections-and-Programs).

> 要退出调试一个分叉的进程，您可以使用`detach inferiors`命令(允许它独立运行)从中分离，或使用`kill inferiors`命令将其杀死。请参阅[调试多个下属连接和程序](Inferiors-Connections-and-Programs.html#Inferiors-Connections-and-Programs)。


If you ask to debug a child process and a `vfork` is followed by an `exec`, [GDB] executes the new target up to the first breakpoint in the new target. If you have a breakpoint set on `main` in your original program, the breakpoint will also be set on the child process's `main`.

> 如果您要求调试子进程，并且 `vfork` 后跟着一个 `exec`，[GDB] 将在新目标中执行到第一个断点。如果在原始程序的`main`上设置了断点，则子进程的`main`也将设置断点。


On some systems, when a child process is spawned by `vfork`, you cannot debug the child or parent until an `exec` call completes.

> 在某些系统中，当一个子进程被`vfork`创建时，在`exec`调用完成之前，你无法调试子进程或父进程。


If you issue a `run` command to [GDB] discards the symbols of the previous executable image. You can change this behaviour with the `set follow-exec-mode` command.

> 如果你向GDB发出“运行”命令，它会丢弃之前可执行映像中的符号。你可以使用“set follow-exec-mode”命令改变这种行为。

`set follow-exec-mode mode`


Set debugger response to a program call of `exec`. An `exec` call replaces the program image of a process.

> 将调试器响应设置为对`exec`程序调用的响应。`exec`调用替换了进程的程序图像。

`follow-exec-mode` can be:

`new`


:   [GDB] creates a new inferior and rebinds the process to this new inferior. The program the process was running before the `exec` call can be restarted afterwards by restarting the original inferior.

> GDB创建一个新的次级进程，并将进程重新绑定到这个新的次级进程。在`exec`调用之前进程正在运行的程序可以通过重新启动原来的次级进程来重新启动。

```
For example:

::: smallexample
``` smallexample
(gdb) info inferiors
(gdb) info inferior
  Id   Description   Executable
* 1    <null>        prog1
(gdb) run
process 12020 is executing new program: prog2
Program exited normally.
(gdb) info inferiors
  Id   Description   Executable
  1    <null>        prog1
* 2    <null>        prog2
```

:::

```

`same`


:   [GDB] keeps the process bound to the same inferior. The new executable image replaces the previous executable loaded in the inferior. Restarting the inferior after the `exec` call, with e.g., the `run` command, restarts the executable the process was running after the `exec` call. This is the default mode.

> GDB保持进程与同一个次级进程绑定。新的可执行映像替换了次级进程中加载的先前可执行文件。在`exec`调用之后，使用例如`run`命令重新启动次级进程，将重新启动`exec`调用之后进程正在运行的可执行文件。这是默认模式。

```

For example:

::: smallexample

```bash
(gdb) info inferiors
  Id   Description   Executable
* 1    <null>        prog1
(gdb) run
process 12020 is executing new program: prog2
Program exited normally.
(gdb) info inferiors
  Id   Description   Executable
* 1    <null>        prog2
```

:::

```

`follow-exec-mode` is supported in native mode and `target extended-remote` mode.


You can use the `catch` command to make [GDB] stop whenever a `fork`, `vfork`, or `exec` call is made. See [Setting Catchpoints](Set-Catchpoints.html#Set-Catchpoints).

> 你可以使用`catch`命令来让GDB在每次`fork`、`vfork`或`exec`调用时停止。请参阅[设置捕获点](Set-Catchpoints.html#Set-Catchpoints)。

---

::: header
Next: [Checkpoint/Restart](Checkpoint_002fRestart.html#Checkpoint_002fRestart)]
:::
```
