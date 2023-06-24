---
tip: translate by openai@2023-06-24 00:47:43
...
---
description: OS Information (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: OS Information (Debugging with GDB)
lang: en
resource-type: document
title: OS Information (Debugging with GDB)
---
::: header
Next: [Memory Region Attributes](Memory-Region-Attributes.html#Memory-Region-Attributes)]
:::

---

### 10.17 Operating System Auxiliary Information


[GDB] provides interfaces to useful OS facilities that can help you debug your program.

> [GDB] 提供了可以帮助您调试程序的有用操作系统功能的接口。


Some operating systems supply an *auxiliary vector* to programs at startup. This is akin to the arguments and environment that you specify for a program, but contains a system-dependent variety of binary values that tell system libraries important details about the hardware, operating system, and process. Each value's purpose is identified by an integer tag; the meanings are well-known but system-specific. Depending on the configuration and operating system facilities, [GDB]' packet, see [qXfer auxiliary vector read](General-Query-Packets.html#qXfer-auxiliary-vector-read).

> 一些操作系统在启动时向程序提供*辅助向量*。这类似于您为程序指定的参数和环境，但包含系统特定的二进制值，可告知系统库有关硬件、操作系统和进程的重要信息。每个值的用途由整数标记确定；其意义是众所周知的，但是系统特定的。根据配置和操作系统功能，可以查看[GDB]的数据包，请参见[qXfer auxiliary vector read](General-Query-Packets.html#qXfer-auxiliary-vector-read)。

`info auxv`


Display the auxiliary vector of the inferior, which can be either a live process or a core dump file. [GDB] displays each value in the most appropriate form for a recognized tag, and in hexadecimal for an unrecognized tag.

> 显示下属的辅助向量，可以是一个活动进程或核心转储文件。 [GDB] 以最适合的形式显示每个识别标记的值，对于未识别的标记，则以十六进制显示。


On some targets, [GDB]' packet, see [qXfer osdata read](General-Query-Packets.html#qXfer-osdata-read).

> 在某些目标上，可以使用[GDB]包，请参见[qXfer osdata read](General-Query-Packets.html#qXfer-osdata-read)。

`info os infotype`

Display OS information of the requested type.

On [GNU] are valid:

`cpus`


Display the list of all CPUs/cores. For each CPU/core, [GDB] prints the available fields from /proc/cpuinfo. For each supported architecture different fields are available. Two common entries are processor which gives CPU number and bogomips; a system constant that is calculated during kernel initialization.

> 显示所有CPU/核心的列表。对于每个CPU/核心，[GDB]会从/proc/cpuinfo中打印出可用的字段。对于每个支持的架构，可用的字段有所不同。两个常见的条目是processor，它给出CPU编号，以及bogomips，它是在内核初始化期间计算出来的系统常量。

`files`


Display the list of open file descriptors on the target. For each file descriptor, [GDB] prints the identifier of the process owning the descriptor, the command of the owning process, the value of the descriptor, and the target of the descriptor.

> 在目标上显示打开的文件描述符列表。对于每个文件描述符，[GDB]打印拥有该描述符的进程的标识符、拥有该进程的命令、描述符的值以及描述符的目标。

`modules`


Display the list of all loaded kernel modules on the target. For each module, [GDB] prints the module name, the size of the module in bytes, the number of times the module is used, the dependencies of the module, the status of the module, and the address of the loaded module in memory.

> 显示目标上加载的所有内核模块的列表。对于每个模块，[GDB]将打印模块名称，模块大小（以字节为单位），模块使用次数，模块的依赖关系，模块的状态以及内存中加载模块的地址。

`msg`


Display the list of all System V message queues on the target. For each message queue, [GDB] prints the message queue key, the message queue identifier, the access permissions, the current number of bytes on the queue, the current number of messages on the queue, the processes that last sent and received a message on the queue, the user and group of the owner and creator of the message queue, the times at which a message was last sent and received on the queue, and the time at which the message queue was last changed.

> 显示目标上所有System V消息队列的列表。对于每个消息队列，[GDB]将打印消息队列键、消息队列标识符、访问权限、队列上当前字节数、消息队列上当前消息数、最后发送和接收消息的进程、拥有者和创建者的用户和组、最后发送和接收消息的时间以及消息队列最后一次更改的时间。

`processes`


Display the list of processes on the target. For each process, [GDB]/Linux documentation.)

> 显示目标上的进程列表。对于每个进程，请参阅[GDB]/Linux文档。

`procgroups`


Display the list of process groups on the target. For each process, [GDB] prints the identifier of the process group that it belongs to, the command corresponding to the process group leader, the process identifier, and the command line of the process. The list is sorted first by the process group identifier, then by the process identifier, so that processes belonging to the same process group are grouped together and the process group leader is listed first.

> 在目标上显示进程组列表。对于每个进程，[GDB]会打印它所属的进程组的标识符、进程组领导者对应的命令、进程标识符以及进程的命令行。该列表首先按照进程组标识符排序，然后按照进程标识符排序，因此属于同一进程组的进程被分组在一起，并且进程组领导者列在首位。

`semaphores`


Display the list of all System V semaphore sets on the target. For each semaphore set, [GDB] prints the semaphore set key, the semaphore set identifier, the access permissions, the number of semaphores in the set, the user and group of the owner and creator of the semaphore set, and the times at which the semaphore set was operated upon and changed.

> 显示目标上所有System V信号量集的列表。对于每个信号量集，[GDB]会打印出信号量集键、信号量集标识符、访问权限、信号量集中信号量的数量、信号量集的所有者和创建者的用户和组，以及操作和更改信号量集的时间。

`shm`


Display the list of all System V shared-memory regions on the target. For each shared-memory region, [GDB] prints the region key, the shared-memory identifier, the access permissions, the size of the region, the process that created the region, the process that last attached to or detached from the region, the current number of live attaches to the region, and the times at which the region was last attached to, detach from, and changed.

> 在目标上显示所有System V共享内存区域的列表。对于每个共享内存区域，[GDB]会打印出区域键、共享内存标识符、访问权限、区域大小、创建该区域的进程、最后一次附加或脱离该区域的进程、该区域当前活动附加数、以及该区域最后一次附加、脱离和更改的时间。

`sockets`


Display the list of Internet-domain sockets on the target. For each socket, [GDB] prints the address and port of the local and remote endpoints, the current state of the connection, the creator of the socket, the IP address family of the socket, and the type of the connection.

> 在目标上显示Internet域套接字列表。对于每个套接字，[GDB]将打印本地和远程端点的地址和端口、连接的当前状态、套接字的创建者、套接字的IP地址族以及连接的类型。

`threads`


Display the list of threads running on the target. For each thread, [GDB] prints the identifier of the process that the thread belongs to, the command of the process, the thread identifier, and the processor core that it is currently running on. The main thread of a process is not listed.

> 显示目标上运行的线程列表。 对于每个线程，[GDB]会打印该线程所属进程的标识符、进程的命令、线程标识符以及它当前运行的处理器核心。 不列出进程的主线程。

`info os`


If `infotype`. If the target does not return a list of possible types, this command will report an error.

> 如果`infotype`。如果目标没有返回可能类型的列表，此命令将报告错误。

---

::: header
Next: [Memory Region Attributes](Memory-Region-Attributes.html#Memory-Region-Attributes)]
:::
