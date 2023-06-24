---
tip: translate by openai@2023-06-24 01:20:52
...
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

> 一些操作系统提供接口来获取有关正在运行的进程的除内存和每个线程寄存器状态以外的其他信息。如果[GDB]针对支持的接口的操作系统进行了配置，则可以使用`info proc`命令来报告有关正在运行您的程序的进程或在您的系统上运行的任何进程的信息。


One supported interface is a facility called '`/proc`/Linux and Solaris systems.

> 一种支持的接口是称为“/proc”的设施，适用于Linux和Solaris系统。


On FreeBSD and NetBSD systems, system control nodes are used to query process information.

> 在FreeBSD和NetBSD系统中，使用系统控制节点来查询进程信息。


In addition, some systems may provide additional process information in core files. Note that a core file may include a subset of the information available from a live process. Process information is currently available from cores created on [GNU]/Linux and FreeBSD systems.

> 此外，某些系统可能会在核心文件中提供额外的进程信息。请注意，核心文件可能只包含从活动进程获取的信息的一个子集。目前可以从在[GNU]/Linux和FreeBSD系统上创建的核心文件获取进程信息。

`info proc`

`info proc process-id`


Summarize available information about a process. If a process ID is specified by `process-id`, display information about that process; otherwise display information about the program being debugged. The summary includes the debugged process ID, the command line used to invoke it, its current working directory, and its executable file's absolute file name.

> 如果指定了进程ID `process-id`，则显示该进程的信息；否则显示被调试程序的信息。摘要包括被调试进程ID、用于调用它的命令行、其当前工作目录以及其可执行文件的绝对文件名。


On some systems, `process-id` will interpret the number as a process ID rather than a thread ID).

> 在某些系统中，`process-id`会将数字解释为进程ID而不是线程ID。

`info proc cmdline`


Show the original command line of the process. This command is supported on [GNU]/Linux, FreeBSD and NetBSD.

> 显示进程的原始命令行。此命令在[GNU]/Linux、FreeBSD和NetBSD上支持。

`info proc cwd`


Show the current working directory of the process. This command is supported on [GNU]/Linux, FreeBSD and NetBSD.

> 显示当前进程的工作目录。此命令在[GNU]/Linux、FreeBSD和NetBSD上支持。

`info proc exe`


Show the name of executable of the process. This command is supported on [GNU]/Linux, FreeBSD and NetBSD.

> 显示进程的可执行文件名称。此命令在[GNU]/Linux、FreeBSD和NetBSD上受支持。

`info proc files`


Show the file descriptors open by the process. For each open file descriptor, [GDB] shows its number, type (file, directory, character device, socket), file pointer offset, and the name of the resource open on the descriptor. The resource name can be a file name (for files, directories, and devices) or a protocol followed by socket address (for network connections). This command is supported on FreeBSD.

> 显示进程打开的文件描述符。对于每个打开的文件描述符，[GDB]会显示其编号、类型（文件、目录、字符设备、套接字）、文件指针偏移量以及打开该描述符的资源名称。资源名称可以是文件名（用于文件、目录和设备）或者是协议名称加上套接字地址（用于网络连接）。此命令在FreeBSD上受支持。


This example shows the open file descriptors for a process using a tty for standard input and output as well as two network sockets:

> 这个例子展示了一个进程使用终端设备作为标准输入和输出以及两个网络套接字的打开文件描述符：

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

> 在进程中报告可访问的内存地址空间范围。在Solaris、FreeBSD和NetBSD系统中，每个内存范围包括有关进程是否具有对每个范围的读取、写入或执行访问权限的信息。在[GNU]/Linux、FreeBSD和NetBSD系统中，每个内存范围包括映射到该范围的对象文件。

`info proc stat`

`info proc status`


Show additional process-related information, including the user ID and group ID; virtual memory usage; the signals that are pending, blocked, and ignored; its TTY; its consumption of system and user time; its stack size; its '`nice`/Linux, FreeBSD and NetBSD.

> 显示附加的与进程相关的信息，包括用户ID和组ID；虚拟内存使用情况；挂起、阻塞和忽略的信号；它的TTY；它消耗的系统和用户时间；它的堆栈大小；它的'nice' / Linux，FreeBSD和NetBSD。

For [GNU] from your shell prompt).


For FreeBSD and NetBSD systems, `info proc stat` is an alias for `info proc status`.

> 对于FreeBSD和NetBSD系统，`info proc stat`是`info proc status`的别名。

`info proc all`


Show all the information about the process described under all of the above `info proc` subcommands.

> 显示所有上述`info proc`子命令描述的进程的信息。

`set procfs-trace`

This command enables and disables tracing of `procfs` API calls.

`show procfs-trace`

Show the current state of `procfs` API call tracing.

`set procfs-file file`


Tell [GDB] appends the trace info to the previous contents of the file. The default is to display the trace on the standard output.

> 告诉GDB，将跟踪信息附加到文件的先前内容。默认情况下，将跟踪信息显示在标准输出上。

`show procfs-file`

Show the file to which `procfs` API trace is written.

`proc-trace-entry`

`proc-trace-exit`

`proc-untrace-entry`

`proc-untrace-exit`


These commands enable and disable tracing of entries into and exits from the `syscall` interface.

> 这些命令可以启用和禁用对`syscall`接口的进入和退出的跟踪。

`info pidlist`


For QNX Neutrino only, this command displays the list of all the processes and all the threads within each process.

> 此命令仅针对QNX Neutrino，用于显示所有进程及每个进程中的所有线程的列表。

`info meminfo`

For QNX Neutrino only, this command displays the list of all mapinfos.

---

::: header
Next: [DJGPP Native](DJGPP-Native.html#DJGPP-Native)]
:::
