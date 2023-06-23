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

To use the server, you must tell it how to communicate with [GDB]; the name of your program; and the arguments for your program. The usual syntax is:

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

The `stdio` connection is useful when starting `gdbserver` with ssh:

::: smallexample

```bash
(gdb) target remote | ssh -T hostname gdbserver - hello
```

:::

The '`-T`' option to ssh is provided because we don't need a remote pty, and we don't want escape-character handling. Ssh does this by default when a command is provided, the flag is provided to make it explicit. You could elide it if you want to.

Programs started with stdio-connected gdbserver have `/dev/null` for `stdin`, and `stdout`,`stderr` are sent back to gdb for display through a pipe connected to gdbserver. Both `stdout` and `stderr` use the same pipe.

#### 20.3.1.1 Attaching to a Running Program

On some targets, `gdbserver` can also attach to running programs. This is accomplished via the `--attach` argument. The syntax is:

::: smallexample

```bash
target> gdbserver --attach comm pid
```

:::

`pid` is the process ID of a currently running process. It isn't necessary to point `gdbserver` at a binary for the running process.

In `target extended-remote` mode, you can also attach using the [GDB] attach command (see [Attaching in Types of Remote Connections](Connecting.html#Attaching-in-Types-of-Remote-Connections)).

You can debug processes by name instead of process ID if your target has the `pidof` utility:

::: smallexample

```bash
target> gdbserver --attach comm `pidof program`
```

:::

In case more than one copy of `program` has multiple threads, most versions of `pidof` support the `-s` option to only return the first process ID.

#### 20.3.1.2 TCP port allocation lifecycle of `gdbserver`

This section applies only when `gdbserver` is run to listen on a TCP port.

`gdbserver` normally terminates after all of its debugged processes have terminated in [target remote] mode.

When `gdbserver` stays running, [GDB] can be connected at a time.

By default, `gdbserver` keeps the listening TCP port open, so that subsequent connections are possible. However, if you start `gdbserver` with the `--once` option allows reusing the same port number for connecting to multiple instances of `gdbserver` running on the same host, since each instance closes its port after the first connection.

#### 20.3.1.3 Other Command-Line Arguments for `gdbserver`

You can use the `--multi` option to start `gdbserver` without specifying a program to debug or a process to attach to. Then you can attach in `target extended-remote` mode and run or attach to a program. For more information, see [\--multi Option in Types of Remote Connnections](Connecting.html#g_t_002d_002dmulti-Option-in-Types-of-Remote-Connnections).

The `--debug`. These options are intended for `gdbserver` development and for bug reports to the developers.

The `--debug-format=option1[,option2,...]` option tells `gdbserver` to include additional information in each output. Possible options are:

`none`

:   Turn off all extra information in debugging output.

`all`

:   Turn on all extra information in debugging output.

`timestamps`

:   Include a timestamp in each line of debugging output.

Options are processed in order. Thus, for example, if `none` appears last then no additional information is added to debugging output.

The `--wrapper` indicating the end of the wrapper arguments.

`gdbserver` runs the specified wrapper program with a combined command line including the wrapper arguments, then the name of the program to debug, then any arguments to the program. The wrapper runs until it executes your program, and then [GDB] gains control.

You can use any program that eventually calls `execve` with its arguments as a wrapper. Several standard Unix utilities do this, e.g. `env` and `nohup`. Any Unix shell script ending with `exec "$@"` will also work.

For example, you can use `env` to pass an environment variable to the debugged program, without setting the variable in `gdbserver`'s environment:

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
- Connect to your target (see [Connecting to a Remote Target](Connecting.html#Connecting)). For TCP connections, you must start up `gdbserver` prior to using the `target` command. Otherwise you may get an error whose text depends on the host system, but which usually looks something like '`Connection refused` when using `target remote` mode, since the program is already on the target.

#### 20.3.3 Monitor Commands for `gdbserver`

During a [GDB] session using `gdbserver`, you can use the `monitor` command to send special requests to `gdbserver`. Here are the available commands.

`monitor help`

:   List the available monitor commands.

`monitor set debug 0`
`monitor set debug 1`

:   Disable or enable general debugging messages.

`monitor set remote-debug 0`
`monitor set remote-debug 1`

:   Disable or enable specific debugging messages associated with the remote protocol (see [Remote Protocol](Remote-Protocol.html#Remote-Protocol)).

`monitor set debug-file filename`
`monitor set debug-file`

:   Send any debug output to the given file, or to stderr.

`monitor set debug-format option1[,option2,...]`

:   Specify additional text to add to debugging messages. Possible options are:

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

#### 20.3.4 Tracepoints support in `gdbserver`

On some targets, `gdbserver` supports tracepoints, fast tracepoints and static tracepoints.

For fast or static tracepoints to work, a special library called the *in-process agent* (IPA), must be loaded in the inferior process. This library is built and distributed as an integral part of `gdbserver`. In addition, support for static tracepoints requires building the in-process agent library with static tracepoints support. At present, the UST (LTTng Userspace Tracer, [http://lttng.org/ust](http://lttng.org/ust)) tracing engine is supported. This support is automatically available if UST development headers are found in the standard include path when `gdbserver` is built, or if `gdbserver` was explicitly configured using `--with-ust`.

There are several ways to load the in-process agent in your program:

`Specifying it as dependency at link time`

:   You can link your program dynamically with the in-process agent library. On most systems, this is accomplished by adding `-linproctrace` to the link command.

`Using the system's preloading mechanisms`

:   You can force loading the in-process agent at startup time by using your system's support for preloading shared libraries. Many Unixes support the concept of preloading user defined libraries. In most cases, you do that by specifying `LD_PRELOAD=libinproctrace.so` in the environment. See also the description of `gdbserver`'s `--wrapper` command line option.

`Using GDB to force loading the agent at run time`

:   On some systems, you can force the inferior to load a shared library, by calling a dynamic loader function in the inferior that takes care of dynamically looking up and loading a shared library. On most Unix systems, the function is `dlopen`. You'll use the `call` command for that. For example:

```
::: smallexample
``` smallexample
(gdb) call dlopen ("libinproctrace.so", ...)
```

:::

Note that on most Unix systems, for the `dlopen` function to be available, the program needs to be linked with `-ldl`.

```

On systems that have a userspace dynamic loader, like most Unix systems, when you connect to `gdbserver` using `target remote`, you'll find that the program is stopped at the dynamic loader's entry point, and no shared library has been loaded in the program's address space yet, including the in-process agent. In that case, before being able to use any of the fast or static tracepoints features, you need to let the loader run and load the shared libraries. The simplest way to do that is to run the program to the main procedure. E.g., if debugging a C or C++ program, start `gdbserver` like so:

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

::: footnote

---

#### Footnotes

### [(16)](#DOCF16)

If you choose a port number that conflicts with another service, `gdbserver` prints an error message and exits.
:::

---

::: header
Next: [Remote Configuration](Remote-Configuration.html#Remote-Configuration)]
:::
