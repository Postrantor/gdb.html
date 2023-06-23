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

#### 20.1.1 Types of Remote Connections

[GDB] supports two types of remote connections, `target remote` mode and `target extended-remote` mode. Note that many remote targets support only `target remote` mode. There are several major differences between the two types of connections, enumerated here:

Result of detach or program exit

**With target remote mode:** When the debugged program exits or you detach from it, [GDB] disconnects from the target. When using `gdbserver`, `gdbserver` will exit.

**With target extended-remote mode:** When the debugged program exits or you detach from it, [GDB] remains connected to the target, even though no program is running. You can rerun the program, attach to a running program, or use `monitor` commands specific to the target.

When using `gdbserver` in this case, it does not exit unless it was invoked using the `--once` option was not used, you can ask `gdbserver` to exit using the `monitor exit` command (see [Monitor Commands for gdbserver](Server.html#Monitor-Commands-for-gdbserver)).

Specifying the program to debug

For both connection types you use the `file` command to specify the program on the host system. If you are using `gdbserver` there are some differences in how to specify the location of the program on the target.

**With target remote mode:** You must either specify the program to debug on the `gdbserver` command line or use the `--attach` option (see [Attaching to a Running Program](Server.html#Attaching-to-a-program)).

**With target extended-remote mode:** You may specify the program to debug on the `gdbserver` command line, or you can load the program or attach to it using [GDB] commands after connecting to `gdbserver`.

You can start `gdbserver` without supplying an initial command to run or process ID to attach. To do this, use the `--multi` option to `gdbserver` has no influence on that.

The `run` command

**With target remote mode:** The `run` command is not supported. Once a connection has been established, you can use all the usual [GDB].

**With target extended-remote mode:** The `run` command is supported. The `run` command uses the value set by `set remote exec-file` (see [set remote exec-file](Remote-Configuration.html#set-remote-exec_002dfile)) to select the program to run. Command line arguments are supported, except for wildcard expansion and I/O redirection (see [Arguments](Arguments.html#Arguments)).

If you specify the program to debug on the command line, then the `run` command is not required to start execution, and you can resume using commands like [step] as with `target remote` mode.

Attaching

**With target remote mode:** The [GDB] option (see [Running gdbserver](Server.html#Running-gdbserver)).

**With target extended-remote mode:** To attach to a running program, you may use the `attach` command after the connection has been established. If you are using `gdbserver`, you may also invoke `gdbserver` using the `--attach` option (see [Running gdbserver](Server.html#Running-gdbserver)).

Some remote targets allow [GDB] (see [set exec-file-mismatch](Attach.html#set-exec_002dfile_002dmismatch)).

#### 20.1.2 Host and Target Files

[GDB], running on the host, needs access to symbol and debugging information for your program running on the target. This requires access to an unstripped copy of your program, and possibly any associated symbol files. Note that this section applies equally to both `target remote` mode and `target extended-remote` mode.

Some remote targets (see [qXfer executable filename read](General-Query-Packets.html#qXfer-executable-filename-read), and see [Host I/O Packets](Host-I_002fO-Packets.html#Host-I_002fO-Packets)) allow [GDB]. With such a target, if the remote program is unstripped, the only command you need is `target remote` (or `target extended-remote`).

If the remote program is stripped, or the target does not support remote program file access, start up [GDB] locates target libraries.

The symbol file and target libraries must exactly match the executable and libraries on the target, with one exception: the files on the host system should not be stripped, even if the files on the target system are. Mismatched or missing files will lead to confusing results during debugging. On [GNU]/Linux targets, mismatched or missing files may also prevent `gdbserver` from debugging multi-threaded programs.

#### 20.1.3 Remote Connection Commands

[GDB] uses the same protocol for debugging your program; only the medium carrying the debugging packets varies. The `target remote` and `target extended-remote` commands establish a connection to the target. Both commands accept the same arguments, which indicate the medium to use:

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

`disconnect`

The `disconnect` command closes the connection to the target, and the target is generally not resumed. It will wait for [GDB] is again free to connect to another target.

`monitor cmd`

This command allows you to send arbitrary commands directly to the remote monitor. Since [GDB]---you can add new commands that only the external monitor will understand and implement.

---

::: header
Next: [File Transfer](File-Transfer.html#File-Transfer)]
:::
