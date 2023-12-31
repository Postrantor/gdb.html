---
tip: translate by openai@2023-06-24 03:11:31
...
---
description: Starting (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Starting (Debugging with GDB)
lang: en
resource-type: document
title: Starting (Debugging with GDB)
---
::: header
Next: [Arguments](Arguments.html#Arguments)]
:::

---

### 4.2 Starting your Program

`run`

`r`


Use the `run` command to start your program under [GDB]](Invocation.html#Invocation)), or by using the `file` or `exec-file` command (see [Commands to Specify Files](Files.html#Files)).

> 使用`run`命令在[GDB](Invocation.html#Invocation)下启动程序，或者使用`file`或`exec-file`命令（参见[指定文件的命令](Files.html#Files)）。


If you are running your program in an execution environment that supports processes, `run` creates an inferior process and makes that process run your program. In some environments without processes, `run` jumps to the start of your program. Other targets, like '`remote`', are always running. If you get an error message like this one:

> 如果您在支持进程的执行环境中运行程序，则`run`将创建一个次级进程并使该进程运行您的程序。在没有进程的一些环境中，`run`会跳到您程序的开始处。其他目标，如'`remote`'，总是在运行状态。如果您收到类似这样的错误消息：

::: smallexample

```bash
The "remote" target does not support "run".
Try "help target" or "continue".
```

:::


then use `continue` to run your program. You may need `load` first (see [load](Target-Commands.html#load)).

> 然后使用“继续”来运行程序。你可能需要先“加载”（参见[加载](Target-Commands.html#load)）。


The execution of a program is affected by certain information it receives from its superior. [GDB] provides ways to specify this information, which you must do *before* starting your program. (You can change it after starting your program, but such changes only affect your program the next time you start it.) This information may be divided into four categories:

> 在开始程序之前，你必须指定[GDB]提供的一些信息，以影响程序的执行。（你可以在程序开始后更改它，但这些更改只会在下一次开始程序时才会生效。）这些信息可以分为四类：

The *arguments.*


:   Specify the arguments to give your program as the arguments of the `run` command. If a shell is available on your target, the shell is used to pass the arguments, so that you may use normal conventions (such as wildcard expansion or variable substitution) in describing the arguments. In Unix systems, you can control which shell is used with the `SHELL` environment variable. If you do not define `SHELL`, [GDB]). You can disable use of any shell with the `set startup-with-shell` command (see below for details).

> 指定程序的参数作为“运行”命令的参数。如果目标上有shell，则使用shell传递参数，因此您可以在描述参数时使用正常的约定（例如通配符扩展或变量替换）。在Unix系统中，您可以使用“SHELL”环境变量控制使用哪个shell。如果您不定义“SHELL”，[GDB]）。您可以使用“set startup-with-shell”命令禁用任何shell（有关详细信息，请参见下文）。

The *environment.*


:   Your program normally inherits its environment from [GDB] commands `set environment` and `unset environment` to change parts of the environment that affect your program. See [Your Program's Environment](Environment.html#Environment).

> 你的程序通常会从[GDB]命令`set environment`和`unset environment`继承其环境，以改变影响你的程序的环境部分。请参见[你的程序的环境](Environment.html#Environment)。

The *working directory.*


:   You can set your program's working directory with the command [set cwd]'s working directory if native debugging, or the remote server's working directory if remote debugging. See [Your Program's Working Directory](Working-Directory.html#Working-Directory).

> 您可以使用命令[set cwd]来设置程序的工作目录，如果是本地调试则为本地工作目录，如果是远程调试则为远程服务器的工作目录。详情请参见[您的程序的工作目录](Working-Directory.html#Working-Directory)。

The *standard input and output.*


:   Your program normally uses the same device for standard input and standard output as [GDB] is using. You can redirect input and output in the `run` command line, or you can use the `tty` command to set a different device for your program. See [Your Program's Input and Output](Input_002fOutput.html#Input_002fOutput).

> 你的程序通常使用和GDB相同的设备来进行标准输入和标准输出。你可以在`run`命令行中重定向输入和输出，或者你可以使用`tty`命令为你的程序设置不同的设备。请参阅[你的程序的输入和输出](Input_002fOutput.html#Input_002fOutput)。

```


*Warning:* While input and output redirection work, you cannot use pipes to pass the output of the program you are debugging to another program; if you attempt this, [GDB] is likely to wind up debugging the wrong program.
```


When you issue the `run` command, your program begins to execute immediately. See [Stopping and Continuing](Stopping.html#Stopping), for discussion of how to arrange for your program to stop. Once your program has stopped, you may call functions in your program, using the `print` or `call` commands. See [Examining Data](Data.html#Data).

> 当你输入`run`命令时，你的程序将立即开始执行。请参阅[停止和继续](Stopping.html#Stopping)，以讨论如何安排你的程序停止。一旦你的程序停止，你可以使用`print`或`call`命令调用程序中的函数。请参阅[检查数据](Data.html#Data)。


If the modification time of your symbol file has changed since the last time [GDB] tries to retain your current breakpoints.

> 如果你的符号文件的修改时间自上次[GDB]尝试保留当前断点以来已经改变，

`start`


The name of the main procedure can vary from language to language. With C or C++, the main procedure name is always `main`, but other languages such as Ada do not require a specific name for their main procedure. The debugger provides a convenient way to start the execution of the program and to stop at the beginning of the main procedure, depending on the language used.

> 主程序的名称可能因语言而异。对于C或C++来说，主程序的名称总是“main”，但是其他语言，如Ada，不需要为它们的主程序指定一个特定的名称。调试器可以方便地启动程序的执行，并在使用的语言的主程序开始处停止。

The '`start`' command.


Some programs contain an *elaboration* phase where some startup code is executed before the main procedure is called. This depends on the languages used to write your program. In C++, for instance, constructors for static and global objects are executed before `main` is called. It is therefore possible that the debugger stops before reaching the main procedure. However, the temporary breakpoint will remain to halt execution.

> 一些程序包含一个*详细*阶段，在调用主程序之前会执行一些启动代码。这取决于用于编写程序的语言。例如，在C++中，静态和全局对象的构造函数会在调用'main'之前执行。因此，调试器可能会在到达主程序之前停止。但是，临时断点将保留以中止执行。


Specify the arguments to give to your program as arguments to the '`start`'.

> 指定给程序的参数作为'start'的参数。


It is sometimes necessary to debug the program during elaboration. In these cases, using the `start` command would stop the execution of your program too late, as the program would have already completed the elaboration phase. Under these circumstances, either insert breakpoints in your elaboration code before running your program or use the `starti` command.

> 有时在编制过程中需要调试程序。 在这些情况下，使用`start`命令会太晚停止程序的执行，因为程序已经完成了编制阶段。 在这种情况下，在运行程序之前在编制代码中插入断点，或者使用`starti`命令。

`starti`


The '`starti`' command. For programs containing an elaboration phase, the `starti` command will stop execution at the start of the elaboration phase.

> `starti`命令。对于包含一个详细阶段的程序，`starti`命令将在详细阶段开始时停止执行。

`set exec-wrapper wrapper`

`show exec-wrapper`

`unset exec-wrapper`

When '`exec-wrapper` takes control.


You can use any program that eventually calls `execve` with its arguments as a wrapper. Several standard Unix utilities do this, e.g. `env` and `nohup`. Any Unix shell script ending with `exec "$@"` will also work.

> 你可以使用任何最终调用`execve`并传入参数的程序作为一个包装器。有几个标准的Unix实用程序可以做到这一点，例如`env`和`nohup`。任何以`exec "$@"`结尾的Unix shell脚本也可以工作。


For example, you can use `env` to pass an environment variable to the debugged program, without setting the variable in your shell's environment:

> 例如，您可以使用`env`将环境变量传递给调试程序，而无需在shell环境中设置变量：

::: smallexample

```bash
(gdb) set exec-wrapper env 'LD_PRELOAD=libtest.so'
(gdb) run
```

:::


This command is available when debugging locally on most targets, excluding [DJGPP], Cygwin, MS Windows, and QNX Neutrino.

> 此命令在大多数目标上本地调试时可用，但不包括[DJGPP]、Cygwin、MS Windows和QNX Neutrino。

`set startup-with-shell`

`set startup-with-shell on`

`set startup-with-shell off`

`show startup-with-shell`


On Unix systems, by default, if a shell is available on your target, [GDB]) uses it to start your program. Arguments of the `run` command are passed to the shell, which does variable substitution, expands wildcard characters and performs redirection of I/O. In some circumstances, it may be useful to disable such use of a shell, for example, when debugging the shell itself or diagnosing startup failures such as:

> 在Unix系统上，默认情况下，如果目标上有shell，[GDB]就会使用它来启动程序。`run`命令的参数将被传递给shell，它将进行变量替换、扩展通配符字符并执行I/O重定向。在某些情况下，禁用shell的使用可能很有用，例如，在调试shell本身或诊断启动失败时：

::: smallexample

```bash
(gdb) run
Starting program: ./a.out
During startup program terminated with signal SIGSEGV, Segmentation fault.
```

:::


which indicates the shell or the wrapper specified with '`exec-wrapper` for the Z shell, or the file specified in the `BASH_ENV` environment variable for BASH.

> 这表明，对于Z shell，使用'exec-wrapper'指定的外壳或包装器；对于BASH，使用BASH_ENV环境变量指定的文件。

`set auto-connect-native-target`

`set auto-connect-native-target on`

`set auto-connect-native-target off`

`show auto-connect-native-target`


By default, if the current inferior is not connected to any target yet (e.g., with `target remote`), the `run` command starts your program as a native process under [GDB] to not connect to the native target automatically with the `set auto-connect-native-target off` command.

> 默认情况下，如果当前的次级还没有连接到任何目标（例如，使用`target remote`），`run`命令会使用[GDB]将您的程序作为本地进程启动，而不会使用`set auto-connect-native-target off`命令自动连接到本地目标。


If `on`, which is the default, and if the current inferior is not connected to a target already, the `run` command automaticaly connects to the native target, if one is available.

> 如果默认情况下“on”被设置，而且当前的次级设备还没有连接到一个目标，那么`run`命令会自动连接到可用的本地目标。


If `off`, and if the current inferior is not connected to a target already, the `run` command fails with an error:

> 如果设置为“off”，如果当前的次级没有已连接到目标，那么`run`命令将会失败并出现错误。

::: smallexample

```bash
(gdb) run
Don't know how to run.  Try "help target".
```

:::


If the current inferior is already connected to a target, [GDB] always uses it with the `run` command.

> 如果当前的次级已经连接到一个目标，[GDB] 在使用`run`命令时总是会使用它。


In any case, you can explicitly connect to the native target with the `target native` command. For example,

> 无论如何，您都可以使用 `target native` 命令显式连接到本地目标。例如，

::: smallexample

```bash
(gdb) set auto-connect-native-target off
(gdb) run
Don't know how to run.  Try "help target".
(gdb) target native
(gdb) run
Starting program: ./a.out
[Inferior 1 (process 10421) exited normally]
```

:::


In case you connected explicitly to the `native` target, [GDB] remains connected even if all inferiors exit, ready for the next `run` command. Use the `disconnect` command to disconnect.

> 如果您明确连接到`native`目标，[GDB]仍然保持连接，即使所有次级都退出，也准备好下一个`run`命令。使用`disconnect`命令断开连接。


Examples of other commands that likewise respect the `auto-connect-native-target` setting: `attach`, `info proc`, `info os`.

> 例如其他同样遵循`auto-connect-native-target`设置的命令：`attach`、`info proc`、`info os`。

`set disable-randomization`

`set disable-randomization on`


This option (enabled by default in [GDB]) will turn off the native randomization of the virtual address space of the started program. This option is useful for multiple debugging sessions to make the execution better reproducible and memory addresses reusable across debugging sessions.

> 这个选项（默认在GDB中启用）将关闭启动的程序的虚拟地址空间的本机随机化。这个选项对于多次调试会话很有用，可以使执行更加可重现，并且调试会话之间可以重复使用内存地址。


This feature is implemented only on certain targets, including [GNU]/Linux you can get the same behavior using

> 这个功能只在某些目标上实现，包括[GNU]/Linux，你可以得到相同的行为。

::: smallexample

```bash
(gdb) set exec-wrapper setarch `uname -m` -R
```

:::

`set disable-randomization off`


Leave the behavior of the started executable unchanged. Some bugs rear their ugly heads only when the program is loaded at certain addresses. If your bug disappears when you run the program under [GDB] to try to reproduce such elusive bugs.

> 离开已启动可执行文件的行为不变。当程序加载在某些地址时，一些错误会出现。如果你的错误在使用GDB运行程序时消失，请尝试重现这些难以捉摸的错误。


On targets where it is available, virtual address space randomization protects the programs against certain kinds of security attacks. In these cases the attacker needs to know the exact location of a concrete executable code. Randomizing its location makes it impossible to inject jumps misusing a code at its expected addresses.

> 在可用的目标上，虚拟地址空间随机化可以保护程序免受某些安全攻击。在这些情况下，攻击者需要知道具体可执行代码的确切位置。随机化其位置使其无法利用预期地址注入跳转。


Prelinking shared libraries provides a startup performance advantage but it makes addresses in these libraries predictable for privileged processes by having just unprivileged access at the target system. Reading the shared library binary gives enough information for assembling the malicious code misusing it. Still even a prelinked shared library can get loaded at a new random address just requiring the regular relocation process during the startup. Shared libraries not already prelinked are always loaded at a randomly chosen address.

> 预链接共享库可以提供启动性能优势，但是对于只有非特权访问的目标系统，它使这些库中的地址变得可预测。仅通过阅读共享库二进制文件就可以获取足够的信息来构建滥用它的恶意代码。尽管如此，即使是预先链接的共享库也可以在启动过程中被加载到一个新的随机地址，只需要正常的重定位过程即可。未预先链接的共享库总是被加载到一个随机选择的地址。


Position independent executables (PIE) contain position independent code similar to the shared libraries and therefore such executables get loaded at a randomly chosen address upon startup. PIE executables always load even already prelinked shared libraries at a random address. You can build such executable using `gcc -fPIE -pie`.

> 可移植可执行文件（PIE）包含与共享库类似的位置独立代码，因此这样的可执行文件在启动时会被随机加载到一个地址。 PIE可执行文件总是在随机地址上加载已预先链接的共享库。 您可以使用`gcc -fPIE -pie`构建此类可执行文件。


Heap (malloc storage), stack and custom mmap areas are always placed randomly (as long as the randomization is enabled).

> 堆（malloc存储）、栈和自定义mmap区域总是随机放置（只要启用了随机化）。

`show disable-randomization`


Show the current setting of the explicit disable of the native randomization of the virtual address space of the started program.

> 显示已启动程序的虚拟地址空间的显式禁用本机随机化的当前设置。

---

::: header
Next: [Arguments](Arguments.html#Arguments)]
:::
