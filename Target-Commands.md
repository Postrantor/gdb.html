---
tip: translate by openai@2023-06-24 03:44:41
...
---
description: Target Commands (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Target Commands (Debugging with GDB)
lang: en
resource-type: document
title: Target Commands (Debugging with GDB)
---
::: header
Next: [Byte Order](Byte-Order.html#Byte-Order)]
:::

---

### 19.2 Commands for Managing Targets

`target type parameters`


:   Connects the [GDB] to specify the type or protocol of the target machine.

> 将[GDB]连接到指定的目标机器的类型或协议。

```
Further `parameters` are interpreted by the target protocol, but typically include things like device names or host names to connect with, process numbers, and baud rates.

The `target` command does not repeat if you press RET again after executing the command.


```

`help target`


:   Displays the names of all targets available. To display targets currently selected, use either `info target` or `info files` (see [Commands to Specify Files](Files.html#Files)).

> 顯示所有可用目標的名稱。要顯示當前選擇的目標，請使用`info target`或`info files`（請參閱[指定檔案的指令]（Files.html＃Files））。

`help target name`


:   Describe a particular target, including any parameters necessary to select it.

> 描述一个特定的目标，包括选择它所必需的任何参数。

```

```

`set gnutarget args`


:   [GDB] knows whether it is reading an *executable*, a *core*, or a *.o* file; however, you can specify the file format with the `set gnutarget` command. Unlike most `target` commands, with `gnutarget` the `target` refers to a program, not a machine.

> GDB知道它是否正在读取可执行文件、内核文件或.o文件；但是，您可以使用“set gnutarget”命令指定文件格式。与大多数“target”命令不同，使用“gnutarget”时，“target”指的是程序，而不是机器。

```
> *Warning:* To specify a file format with `set gnutarget`, you must know the actual BFD name.

See [Commands to Specify Files](Files.html#Files).


```

`show gnutarget`


:   Use the `show gnutarget` command to display what file format `gnutarget` is set to read. If you have not set `gnutarget`, [GDB]'.

> 使用`show gnutarget`命令显示`gnutarget`设置为读取哪种文件格式。如果没有设置`gnutarget`，[GDB]。


Here are some common targets (available, or not, depending on the GDB configuration):

> 这里有一些常见的目标（根据GDB配置可用或不可用）：

`target exec program`

An executable file. '`target exec program`'.

`target core filename`

A core dump file. '`target core filename`'.

`target remote medium`


A remote system connected to [GDB] for debugging. See [Remote Debugging](Remote-Debugging.html#Remote-Debugging).

> 一个远程系统连接到GDB用于调试。参见远程调试（Remote-Debugging.html#Remote-Debugging）。

For example, if you have a board connected to `/dev/ttya`, you could say:

::: smallexample

```bash
target remote /dev/ttya
```

:::

`target remote` supports the `load` command. This is only useful if you have some other way of getting the stub to the target system, and you can put it somewhere in memory where it won't get clobbered by the download.

`target sim [simargs] …`


Builtin CPU simulator. [GDB] includes simulators for most architectures. In general,

> GDB内置的CPU模拟器。GDB包括大多数架构的模拟器。通常来说，

::: smallexample

```bash
        target sim
        load
        run
```

:::


works; however, you cannot assume that a specific memory map, device drivers, or even basic I/O is available, although some simulators do provide these. For info about any processor-specific simulator details, see the appropriate section in [Embedded Processors](Embedded-Processors.html#Embedded-Processors).

> 然而，您不能假定可以使用特定的存储器映射、设备驱动程序甚至基本I/O，尽管一些模拟器提供了这些功能。有关特定处理器模拟器详细信息，请参阅[嵌入式处理器](Embedded-Processors.html#Embedded-Processors)中的相应部分。

`target native`


Setup for local/native process debugging. Useful to make the `run` command spawn native processes (likewise `attach`, etc.) even when `set auto-connect-native-target` is `off` (see [set auto-connect-native-target](Starting.html#set-auto_002dconnect_002dnative_002dtarget)).

> 设置本地/本机进程调试。有助于即使`set auto-connect-native-target`设置为`off`时，`run`命令仍能生成本机进程（如`attach`等）（参见[set auto-connect-native-target](Starting.html#set-auto_002dconnect_002dnative_002dtarget))。


Different targets are available on different configurations of [GDB]; your configuration may have more or fewer targets.

> 不同配置的[GDB]有不同的目标可用；您的配置可能拥有更多或更少的目标。


Many remote targets require you to download the executable's code once you've successfully established a connection. You may wish to control various aspects of this process.

> 许多远程目标要求您在成功建立连接后下载可执行文件的代码。您可能希望控制此过程的各个方面。

`set hash`

:

```
This command controls whether a hash mark '`#`' is displayed while downloading a file to the remote monitor. If on, a hash mark is displayed after each S-record is successfully downloaded to the monitor.
```

`show hash`

:

```
Show the current status of displaying the hash mark.
```

`set debug monitor`

:

```
Enable or disable display of communications messages between [GDB] and the remote monitor.
```

`show debug monitor`

:

```
Show the current status of displaying communications between [GDB] and the remote monitor.
```

`load filename offset`


Depending on what remote debugging facilities are configured into [GDB], like the `add-symbol-file` command.

> 根据GDB中配置的远程调试功能，比如`add-symbol-file`命令。


If your [GDB] does not have a `load` command, attempting to execute it gets the error message "`You can't do that when your target is …`"

> 如果您的GDB没有`load`命令，尝试执行它会得到错误消息“当目标是...时，您无法执行此操作”


The file is loaded at whatever address is specified in the executable. For some object file formats, you can specify the load address when you link the program; for other formats, like a.out, the object file format specifies a fixed address.

> 文件会加载到可执行文件中指定的地址。对于某些对象文件格式，您可以在链接程序时指定加载地址；而对于其他格式（如a.out），对象文件格式指定了固定的地址。

It is also possible to tell [GDB] must also be provided.


Depending on the remote side capabilities, [GDB] may be able to load programs into flash memory.

> 根据远程端的能力，[GDB]可能能够将程序加载到闪存中。

`load` does not repeat if you press RET again after using it.

`flash-erase`

Erases all known flash memory regions on the target.

---

::: header
Next: [Byte Order](Byte-Order.html#Byte-Order)]
:::
