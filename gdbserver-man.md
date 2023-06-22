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

To use the server, you log on to the target system, and run the `gdbserver` program. You must tell it (a) how to communicate with [GDB], (b) the name of your program, and (c) its arguments. The general syntax is:

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

To use a TCP connection, you could say:

::: smallexample

```bash
target> gdbserver host:2345 emacs foo.txt
```

:::

This says pretty much the same thing as the last example, except that we are going to communicate with the `host` [GDB]s `target remote` command, which will be described shortly. Note that if you chose a port number that conflicts with another service, `gdbserver` will print an error message and exit.

`gdbserver` can also attach to running programs. This is accomplished via the `--attach` argument. The syntax is:

::: smallexample

```bash
target> gdbserver --attach comm pid
```

:::

`pid` is the process ID of a currently running process. It isn't necessary to point `gdbserver` at a binary for the running process.

To start `gdbserver` without supplying an initial command to run or process ID to attach, use the `--multi` to start the program you want to debug.

::: smallexample

```bash
target> gdbserver --multi comm
```

:::

#### Usage (host side)

You need an unstripped copy of the target program on your host system, since [GDB]), or a `HOST:PORT` descriptor. For example:

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

```

::: smallexample

```bash
target> gdbserver --multi comm
```

:::

```

`--debug`

:   Instruct `gdbserver` to display extra status information about the debugging process. This option is intended for `gdbserver` development and for bug reports to the developers.

`--remote-debug`

:   Instruct `gdbserver` to display remote protocol debug output. This option is intended for `gdbserver` development and for bug reports to the developers.

`--debug-file=filename`

:   Instruct `gdbserver` to send any debug output to the given `filename`. This option is intended for `gdbserver` development and for bug reports to the developers.

`--debug-format=option1[,option2,...]`

:   Instruct `gdbserver` to include extra information in each line of debugging output. See [Other Command-Line Arguments for gdbserver](Server.html#Other-Command_002dLine-Arguments-for-gdbserver).

`--wrapper`

:   Specify a wrapper to launch programs for debugging. The option should be followed by the name of the wrapper, then any command-line arguments to pass to the wrapper, then [\--] indicating the end of the wrapper arguments.

`--once`

:   By default, `gdbserver` keeps the listening TCP port open, so that additional connections are possible. However, if you start `gdbserver` with the `--once` session.

---

::: header
Next: [gcore man](gcore-man.html#gcore-man)]
:::
```
