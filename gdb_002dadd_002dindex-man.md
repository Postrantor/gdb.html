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

`gdb-add-index` uses [GDB] and `objdump` found in the `PATH` environment variable. If you want to use different versions of these programs, you can specify them through the `GDB` and `OBJDUMP` environment variables.

See more in [Index Files](Index-Files.html#Index-Files).
