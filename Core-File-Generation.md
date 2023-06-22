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

Occasionally, you may wish to produce a core file of the program you are debugging in order to preserve a snapshot of its state. [GDB] has a special command for that.

`generate-core-file [file]`

`gcore [file]`

Produce a core dump of the inferior process. The optional argument `file` is the inferior process ID.

Note that this command is implemented only for some systems (as of this writing, [GNU]/Linux, FreeBSD, Solaris, and S390).

On [GNU] (see [set dump-excluded-mappings](#set-dump_002dexcluded_002dmappings)).

`set use-coredump-filter on`

`set use-coredump-filter off`

Enable or disable the use of the file `/proc/pid/coredump_filter` is the process ID of a currently running process.

To make use of this feature, you have to write in the `/proc/pid/coredump_filter` file, please refer to the manpage of `core(5)`.

By default, this option is `on`. If this option is turned `off`, [GDB] file and instead uses the same default value as the Linux kernel in order to decide which pages will be dumped in the core dump file. This value is currently `0x33`, which means that bits `0` (anonymous private mappings), `1` (anonymous shared mappings), `4` (ELF headers) and `5` (private huge pages) are active. This will cause these memory mappings to be dumped automatically.

`set dump-excluded-mappings on`

`set dump-excluded-mappings off`

If `on` is specified, [GDB] with the acronym `dd`.

The default value is `off`.

---

::: header
Next: [Character Sets](Character-Sets.html#Character-Sets)]
:::
