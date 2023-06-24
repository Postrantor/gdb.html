---
tip: translate by openai@2023-06-23 23:20:42
...
---
description: Inferiors Connections and Programs (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Inferiors Connections and Programs (Debugging with GDB)
lang: en
resource-type: document
title: Inferiors Connections and Programs (Debugging with GDB)
---
::: header
Next: [Threads](Threads.html#Threads)]
:::

---

### 4.9 Debugging Multiple Inferiors Connections and Programs


[GDB] may even let you debug several programs simultaneously on different remote systems. In the most general case, you can have multiple threads of execution in each of multiple processes, launched from multiple executables, running on different machines.

> GDB甚至可以让你同时调试多个不同远程系统上的程序。在最一般的情况下，你可以在不同机器上从多个可执行文件启动的多个进程中有多个执行线程。


[GDB] represents the state of each program execution with an object called an *inferior*. An inferior typically corresponds to a process, but is more general and applies also to targets that do not have processes. Inferiors may be created before a process runs, and may be retained after a process exits. Inferiors have unique identifiers that are different from process ids. Usually each inferior will also have its own distinct address space, although some embedded targets may have several inferiors running in different parts of a single address space. Each inferior may in turn have multiple threads running in it.

> [GDB] 使用一个叫做“inferior”的对象来表示每个程序执行的状态。inferior通常对应于一个进程，但更加普遍，也适用于没有进程的目标。inferior可以在进程运行之前创建，并且可以在进程退出后保留。inferiors有唯一的标识符，与进程ID不同。通常，每个inferior也将具有其自己的独特地址空间，尽管一些嵌入式目标可能在单个地址空间的不同部分中运行多个inferiors。每个inferior可以又有多个线程在其中运行。


The commands `info inferiors` and `info connections`, which will be introduced below, accept a space-separated *ID list* as their argument specifying one or more elements on which to operate. A list element can be either a single non-negative number, like '`5`'.

> 下面将介绍的命令`info inferiors`和`info connections`接受一个以空格分隔的*ID列表*作为其参数，以指定一个或多个要操作的元素。列表元素可以是单个非负数，如'`5`'。

To find out what inferiors exist at any moment, use `info inferiors`:

`info inferiors`


Print a list of all inferiors currently being managed by [GDB]... can be used to limit the display to just the requested inferiors.

> 打印出[GDB]正在管理的所有下属的列表... 可以用来将显示限制到所请求的下属。

[GDB] displays for each inferior (in this order):

1. the inferior number assigned by [GDB]
2. the target system's inferior identifier

3. the target connection the inferior is bound to, including the unique connection number assigned by [GDB], and the protocol used by the connection.

> 3. 目标连接到较低级别，包括[GDB]分配的唯一连接号以及连接所使用的协议。
4. the name of the executable the inferior is running.

An asterisk '`*` inferior number indicates the current inferior.

For example,

::: smallexample

```bash
(gdb) info inferiors
  Num  Description       Connection                      Executable
* 1    process 3401      1 (native)                      goodbye
  2    process 2307      2 (extended-remote host:10000)  hello
```

:::

To get information about the current inferior, use `inferior`:

`inferior`

Shows information about the current inferior.

For example,

::: smallexample

```bash
(gdb) inferior
[Current inferior is 1 [process 3401] (helloworld)]
```

:::


To find out what open target connections exist at any moment, use `info connections`:

> 要查看当前存在哪些开放的目标连接，请使用`info connections`：

`info connections`


Print a list of all open target connections currently being managed by [GDB]... can be used to limit the display to just the requested connections.

> 打印出由GDB管理的所有打开的目标连接的列表... 可用于将显示限制为仅请求的连接。

[GDB] displays for each connection (in this order):

1. the connection number assigned by [GDB].
2. the protocol used by the connection.
3. a textual description of the protocol used by the connection.


An asterisk '`*`' preceding the connection number indicates the connection of the current inferior.

> 一个前缀在连接号前的星号 '*' 表示当前较低级别的连接。

For example,

::: smallexample

```bash
(gdb) info connections
  Num  What                        Description
* 1    extended-remote host:10000  Extended remote serial target in gdb-specific protocol
  2    native                      Native process
  3    core                        Local core dump file
```

:::

To switch focus between inferiors, use the `inferior` command:

`inferior infno`

Make inferior number `infno`' display.


The debugger convenience variable '`$_inferior`' contains the number of the current inferior. You may find this useful in writing breakpoint conditional expressions, command scripts, and so forth. See [Convenience Variables](Convenience-Vars.html#Convenience-Vars), for general information on convenience variables.

> 调试器便利变量'$_inferior'包含当前次级的数字。您可能会在编写断点条件表达式、命令脚本等时发现它有用。有关便利变量的一般信息，请参阅[便利变量](Convenience-Vars.html#Convenience-Vars)。


You can get multiple executables into a debugging session via the `add-inferior` and `clone-inferior` commands. On some systems [GDB] can add inferiors to the debug session automatically by following calls to `fork` and `exec`. To remove inferiors from the debugging session use the `remove-inferiors` command.

> 你可以通过`add-inferior`和`clone-inferior`命令将多个可执行文件添加到调试会话中。在某些系统上，[GDB]可以通过跟踪调用`fork`和`exec`自动添加inferiors到调试会话中。要从调试会话中删除inferiors，请使用`remove-inferiors`命令。

`add-inferior [ -copies n ] [ -exec executable ] [-no-connection ]`


Adds `n` defaults to 1. If no executable is specified, the inferiors begins empty, with no program. You can still assign or change the program assigned to the inferior at any time by using the `file` command with the executable name as its argument.

> 加入`n`，默认值为1。如果没有指定可执行文件，下属开始为空，没有程序。您仍然可以通过使用`file`命令并将可执行文件名作为其参数，随时将程序分配给下属。


By default, the new inferior begins connected to the same target connection as the current inferior. For example, if the current inferior was connected to `gdbserver` with `target remote`, then the new inferior will be connected to the same `gdbserver` instance. The '`-no-connection`' option starts the new inferior with no connection yet. You can then for example use the `target remote` command to connect to some other `gdbserver` instance, use `run` to spawn a local program, etc.

> 默认情况下，新的次要进程将与当前次要进程相同的目标连接相连。例如，如果当前次要进程与`gdbserver`使用`target remote`连接，那么新的次要进程将与相同的`gdbserver`实例连接。'`-no-connection`'选项将新的次要进程以没有连接的方式启动。然后，您可以使用`target remote`命令连接到其他`gdbserver`实例，使用`run`来产生本地程序等等。

`clone-inferior [ -copies n ] [ infno ]`


Adds `n` properties from the current inferior to the new one. It also propagates changes the user made to environment variables using the `set environment` and `unset environment` commands. This is a convenient command when you want to run another instance of the inferior you are debugging.

> 添加`n`个属性从当前的次级到新的。它还传播用户使用`set environment`和`unset environment`命令对环境变量所做的更改。当您想运行调试的另一个次级实例时，这是一个方便的命令。

::: smallexample

```bash
(gdb) info inferiors
  Num  Description       Connection   Executable
* 1    process 29964     1 (native)   helloworld
(gdb) clone-inferior
Added inferior 2.
1 inferiors added.
(gdb) info inferiors
  Num  Description       Connection   Executable
* 1    process 29964     1 (native)   helloworld
  2    <null>            1 (native)   helloworld
```

:::

You can now simply switch focus to inferior 2 and run it.

`remove-inferiors infno…`


Removes the inferior or inferiors `infno`.... It is not possible to remove an inferior that is running with this command. For those, use the `kill` or `detach` command first.

> 移除次级或次级`infno`.... 无法使用此命令移除正在运行的次级。 对于那些，请先使用`kill`或`detach`命令。


To quit debugging one of the running inferiors that is not the current inferior, you can either detach from it by using the `detach inferior` command (allowing it to run independently), or kill it using the `kill inferiors` command:

> 要退出调试当前不是正在运行的次级程序，您可以使用`detach inferior`命令从中分离（允许其独立运行），或使用`kill inferiors`命令杀死它。

`detach inferior infno…`

Detach from the inferior or inferiors identified by [GDB]'.

`kill inferiors infno…`

Kill the inferior or inferiors identified by [GDB]'.


After the successful completion of a command such as `detach`, `detach inferiors`, `kill` or `kill inferiors`, or after a normal process exit, the inferior is still valid and listed with `info inferiors`, ready to be restarted.

> 在成功完成`detach`、`detach inferiors`、`kill`或`kill inferiors`等命令，或正常进程退出后，下级仍有效，可以使用`info inferiors`列出，准备重新启动。


To be notified when inferiors are started or exit under [GDB]'s control use `set print inferior-events`:

> 当GDB控制下的下属被启动或退出时，使用`set print inferior-events`可以收到通知。

`set print inferior-events`

`set print inferior-events on`

`set print inferior-events off`


The `set print inferior-events` command allows you to enable or disable printing of messages when [GDB] notices that new inferiors have started or that inferiors have exited or have been detached. By default, these messages will be printed.

> `命令`set print inferior-events`允许您启用或禁用在[GDB]注意到新的次级已启动或次级已退出或已被分离时打印消息的功能。默认情况下，这些消息将被打印。

`show print inferior-events`


Show whether messages will be printed when [GDB] detects that inferiors have started, exited or have been detached.

> 当[GDB]检测到下位机已启动、退出或脱离时，显示是否将打印消息。


Many commands will work the same with multiple programs as with a single program: e.g., `print myglobal` will simply display the value of `myglobal` in the current inferior.

> 许多命令可以在多个程序中与单个程序一样工作：例如，“打印myglobal”将在当前的次级程序中简单地显示myglobal的值。


Occasionally, when debugging [GDB] itself, it may be useful to get more info about the relationship of inferiors, programs, address spaces in a debug session. You can do that with the `maint info program-spaces` command.

> 在调试GDB本身时，有时可能有用的是了解调试会话中次要程序、程序空间和地址空间之间的关系。您可以使用`maint info program-spaces`命令来完成这项操作。

`maint info program-spaces`

Print a list of all program spaces currently being managed by [GDB].

[GDB] displays for each program space (in this order):

1. the program space number assigned by [GDB]

2. the name of the executable loaded into the program space, with e.g., the `file` command.

> 启动程序空间中加载的可执行文件的名称，例如使用`file`命令。

3. the name of the core file loaded into the program space, with e.g., the `core-file` command.

> 命令`core-file`加载到程序空间的核心文件的名称。


An asterisk '`*` program space number indicates the current program space.

> 一个星号'*'程序空间号表示当前程序空间。


In addition, below each program space line, [GDB] prints extra information that isn't suitable to display in tabular form. For example, the list of inferiors bound to the program space.

> 此外，在每个程序空间行下方，[GDB]会打印出不适合以表格形式显示的额外信息。例如，与程序空间绑定的次级列表。

::: smallexample

```bash
(gdb) maint info program-spaces
  Id   Executable        Core File
* 1    hello
  2    goodbye
        Bound inferiors: ID 1 (process 21561)
```

:::


Here we can see that no inferior is running the program `hello`, while `process 21561` is running the program `goodbye`. On some targets, it is possible that multiple inferiors are bound to the same program space. The most common example is that of debugging both the parent and child processes of a `vfork` call. For example,

> 在这里，我们可以看到没有次等的程序正在运行程序“hello”，而“进程21561”正在运行程序“goodbye”。在某些目标上，有可能多个次等的程序都绑定到同一个程序空间。最常见的例子是调试`vfork`调用的父进程和子进程。例如，

::: smallexample

```bash
(gdb) maint info program-spaces
  Id   Executable        Core File
* 1    vfork-test
        Bound inferiors: ID 2 (process 18050), ID 1 (process 18045)
```

:::


Here, both inferior 2 and inferior 1 are running in the same program space as a result of inferior 1 having executed a `vfork` call.

> 在这里，由于次级1执行了`vfork`调用，次级2和次级1都在同一程序空间中运行。

---

::: header
Next: [Threads](Threads.html#Threads)]
:::
