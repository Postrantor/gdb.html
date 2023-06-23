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

```
Further `parameters` are interpreted by the target protocol, but typically include things like device names or host names to connect with, process numbers, and baud rates.

The `target` command does not repeat if you press RET again after executing the command.


```

`help target`

:   Displays the names of all targets available. To display targets currently selected, use either `info target` or `info files` (see [Commands to Specify Files](Files.html#Files)).

`help target name`

:   Describe a particular target, including any parameters necessary to select it.

```

```

`set gnutarget args`

:   [GDB] knows whether it is reading an *executable*, a *core*, or a *.o* file; however, you can specify the file format with the `set gnutarget` command. Unlike most `target` commands, with `gnutarget` the `target` refers to a program, not a machine.

```
> *Warning:* To specify a file format with `set gnutarget`, you must know the actual BFD name.

See [Commands to Specify Files](Files.html#Files).


```

`show gnutarget`

:   Use the `show gnutarget` command to display what file format `gnutarget` is set to read. If you have not set `gnutarget`, [GDB]'.

Here are some common targets (available, or not, depending on the GDB configuration):

`target exec program`

An executable file. '`target exec program`'.

`target core filename`

A core dump file. '`target core filename`'.

`target remote medium`

A remote system connected to [GDB] for debugging. See [Remote Debugging](Remote-Debugging.html#Remote-Debugging).

For example, if you have a board connected to `/dev/ttya`, you could say:

::: smallexample

```bash
target remote /dev/ttya
```

:::

`target remote` supports the `load` command. This is only useful if you have some other way of getting the stub to the target system, and you can put it somewhere in memory where it won't get clobbered by the download.

`target sim [simargs] …`

Builtin CPU simulator. [GDB] includes simulators for most architectures. In general,

::: smallexample

```bash
        target sim
        load
        run
```

:::

works; however, you cannot assume that a specific memory map, device drivers, or even basic I/O is available, although some simulators do provide these. For info about any processor-specific simulator details, see the appropriate section in [Embedded Processors](Embedded-Processors.html#Embedded-Processors).

`target native`

Setup for local/native process debugging. Useful to make the `run` command spawn native processes (likewise `attach`, etc.) even when `set auto-connect-native-target` is `off` (see [set auto-connect-native-target](Starting.html#set-auto_002dconnect_002dnative_002dtarget)).

Different targets are available on different configurations of [GDB]; your configuration may have more or fewer targets.

Many remote targets require you to download the executable's code once you've successfully established a connection. You may wish to control various aspects of this process.

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

If your [GDB] does not have a `load` command, attempting to execute it gets the error message "`You can't do that when your target is …`"

The file is loaded at whatever address is specified in the executable. For some object file formats, you can specify the load address when you link the program; for other formats, like a.out, the object file format specifies a fixed address.

It is also possible to tell [GDB] must also be provided.

Depending on the remote side capabilities, [GDB] may be able to load programs into flash memory.

`load` does not repeat if you press RET again after using it.

`flash-erase`

Erases all known flash memory regions on the target.

---

::: header
Next: [Byte Order](Byte-Order.html#Byte-Order)]
:::
