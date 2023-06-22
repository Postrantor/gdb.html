---
description: Process Information (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Process Information (Debugging with GDB)
lang: en
resource-type: document
title: Process Information (Debugging with GDB)
---
::: header
Next: [DJGPP Native](DJGPP-Native.html#DJGPP-Native)]
:::

---

#### 21.1.2 Process Information

Some operating systems provide interfaces to fetch additional information about running processes beyond memory and per-thread register state. If [GDB] is configured for an operating system with a supported interface, the command `info proc` is available to report information about the process running your program, or about any process running on your system.

One supported interface is a facility called '`/proc`/Linux and Solaris systems.

On FreeBSD and NetBSD systems, system control nodes are used to query process information.

In addition, some systems may provide additional process information in core files. Note that a core file may include a subset of the information available from a live process. Process information is currently available from cores created on [GNU]/Linux and FreeBSD systems.

`info proc`

`info proc process-id`

Summarize available information about a process. If a process ID is specified by `process-id`, display information about that process; otherwise display information about the program being debugged. The summary includes the debugged process ID, the command line used to invoke it, its current working directory, and its executable file's absolute file name.

On some systems, `process-id` will interpret the number as a process ID rather than a thread ID).

`info proc cmdline`

Show the original command line of the process. This command is supported on [GNU]/Linux, FreeBSD and NetBSD.

`info proc cwd`

Show the current working directory of the process. This command is supported on [GNU]/Linux, FreeBSD and NetBSD.

`info proc exe`

Show the name of executable of the process. This command is supported on [GNU]/Linux, FreeBSD and NetBSD.

`info proc files`

Show the file descriptors open by the process. For each open file descriptor, [GDB] shows its number, type (file, directory, character device, socket), file pointer offset, and the name of the resource open on the descriptor. The resource name can be a file name (for files, directories, and devices) or a protocol followed by socket address (for network connections). This command is supported on FreeBSD.

This example shows the open file descriptors for a process using a tty for standard input and output as well as two network sockets:

::: smallexample

```bash
(gdb) info proc files 22136
process 22136
Open files:

      FD   Type     Offset   Flags   Name
    text   file          - r-------- /usr/bin/ssh
    ctty    chr          - rw------- /dev/pts/20
     cwd    dir          - r-------- /usr/home/john
    root    dir          - r-------- /
       0    chr  0x32933a4 rw------- /dev/pts/20
       1    chr  0x32933a4 rw------- /dev/pts/20
       2    chr  0x32933a4 rw------- /dev/pts/20
       3 socket        0x0 rw----n-- tcp4 10.0.1.2:53014 -> 10.0.1.10:22
       4 socket        0x0 rw------- unix stream:/tmp/ssh-FIt89oAzOn5f/agent.2456
```

:::

`info proc mappings`

Report the memory address space ranges accessible in a process. On Solaris, FreeBSD and NetBSD systems, each memory range includes information on whether the process has read, write, or execute access rights to each range. On [GNU]/Linux, FreeBSD and NetBSD systems, each memory range includes the object file which is mapped to that range.

`info proc stat`

`info proc status`

Show additional process-related information, including the user ID and group ID; virtual memory usage; the signals that are pending, blocked, and ignored; its TTY; its consumption of system and user time; its stack size; its '`nice`/Linux, FreeBSD and NetBSD.

For [GNU] from your shell prompt).

For FreeBSD and NetBSD systems, `info proc stat` is an alias for `info proc status`.

`info proc all`

Show all the information about the process described under all of the above `info proc` subcommands.

`set procfs-trace`

This command enables and disables tracing of `procfs` API calls.

`show procfs-trace`

Show the current state of `procfs` API call tracing.

`set procfs-file file`

Tell [GDB] appends the trace info to the previous contents of the file. The default is to display the trace on the standard output.

`show procfs-file`

Show the file to which `procfs` API trace is written.

`proc-trace-entry`

`proc-trace-exit`

`proc-untrace-entry`

`proc-untrace-exit`

These commands enable and disable tracing of entries into and exits from the `syscall` interface.

`info pidlist`

For QNX Neutrino only, this command displays the list of all the processes and all the threads within each process.

`info meminfo`

For QNX Neutrino only, this command displays the list of all mapinfos.

---

::: header
Next: [DJGPP Native](DJGPP-Native.html#DJGPP-Native)]
:::
