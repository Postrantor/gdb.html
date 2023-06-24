---
tip: translate by openai@2023-06-23 20:04:56
...
---
description: Core File Generation (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Core File Generation (Debugging with GDB)
lang: en
resource-type: document
title: Core File Generation (Debugging with GDB)
---
::: header
Next: [Character Sets](Character-Sets.html#Character-Sets)]
:::

---

### 10.20 How to Produce a Core File from Your Program


A *core file* or *core dump* is a file that records the memory image of a running process and its process status (register values etc.). Its primary use is post-mortem debugging of a program that crashed while it ran outside a debugger. A program that crashes automatically produces a core file, unless this feature is disabled by the user. See [Files](Files.html#Files), for information on invoking [GDB] in the post-mortem debugging mode.

> 一个核心文件或核心转储是记录运行进程的内存映像及其进程状态（寄存器值等）的文件。它的主要用途是在调试器外运行时崩溃的程序的死后调试。程序崩溃时会自动生成核心文件，除非用户禁用此功能。有关在死后调试模式中调用GDB的信息，请参阅文件。


Occasionally, you may wish to produce a core file of the program you are debugging in order to preserve a snapshot of its state. [GDB] has a special command for that.

> 偶尔，您可能希望生成正在调试的程序的核心文件，以保存其状态的快照。[GDB]有一个特殊的命令。

`generate-core-file [file]`

`gcore [file]`


Produce a core dump of the inferior process. The optional argument `file` is the inferior process ID.

> 生成次级进程的核心转储。可选参数`file`是次级进程的ID。


Note that this command is implemented only for some systems (as of this writing, [GNU]/Linux, FreeBSD, Solaris, and S390).

> 注意，此命令目前仅针对某些系统实现（截至本文撰写时，[GNU]/Linux、FreeBSD、Solaris 和 S390）。


On [GNU] (see [set dump-excluded-mappings](#set-dump_002dexcluded_002dmappings)).

> 在[GNU]上（参见[设置dump-excluded-mappings](#set-dump_002dexcluded_002dmappings)）。

`set use-coredump-filter on`

`set use-coredump-filter off`


Enable or disable the use of the file `/proc/pid/coredump_filter` is the process ID of a currently running process.

> 启用或禁用文件“/proc/pid/coredump_filter”的使用是当前正在运行的进程的进程ID。


To make use of this feature, you have to write in the `/proc/pid/coredump_filter` file, please refer to the manpage of `core(5)`.

> 要使用此功能，您必须在`/proc/pid/coredump_filter`文件中编写，请参阅`core(5)`的手册页。


By default, this option is `on`. If this option is turned `off`, [GDB] file and instead uses the same default value as the Linux kernel in order to decide which pages will be dumped in the core dump file. This value is currently `0x33`, which means that bits `0` (anonymous private mappings), `1` (anonymous shared mappings), `4` (ELF headers) and `5` (private huge pages) are active. This will cause these memory mappings to be dumped automatically.

> 默认情况下，此选项为“开启”状态。如果此选项被关闭，[GDB] 将不会使用文件，而是使用与Linux内核相同的默认值来决定哪些页面将被转储到核心转储文件中。当前该值为`0x33`，这意味着位`0`（匿名私有映射），`1`（匿名共享映射），`4`（ELF头）和`5`（私有巨型页面）处于活动状态。这将导致这些内存映射自动被转储。

`set dump-excluded-mappings on`

`set dump-excluded-mappings off`

If `on` is specified, [GDB] with the acronym `dd`.

The default value is `off`.

---

::: header
Next: [Character Sets](Character-Sets.html#Character-Sets)]
:::
