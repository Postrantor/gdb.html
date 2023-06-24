---
tip: translate by openai@2023-06-23 21:40:20
...
---
description: gdb-add-index man (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: gdb-add-index man (Debugging with GDB)
lang: en
resource-type: document
title: gdb-add-index man (Debugging with GDB)
---
::: header
Previous: [gdbinit man](gdbinit-man.html#gdbinit-man)]
:::

---

#### gdb-add-index man

### gdb-add-index

gdb-add-index `filename`

When [GDB] provides a way to build an index, which speeds up startup.


To determine whether a file contains such an index, use the command [readelf -S filename]: the index is stored in a section named `.gdb_index`. The index file can only be produced on systems which use ELF binaries and DWARF debug information (i.e., sections named `.debug_*`).

> 要确定文件是否包含这样的索引，请使用命令[readelf -S filename]：索引存储在名为`.gdb_index`的节中。索引文件只能在使用ELF二进制文件和DWARF调试信息（即名为`.debug_*`的节）的系统上生成。

`gdb-add-index` uses [GDB] and `objdump` found in the `PATH` environment variable. If you want to use different versions of these programs, you can specify them through the `GDB` and `OBJDUMP` environment variables.

See more in [Index Files](Index-Files.html#Index-Files).
