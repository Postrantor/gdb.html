---
description: Init File in the Current Directory (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Init File in the Current Directory (Debugging with GDB)
lang: en
resource-type: document
title: Init File in the Current Directory (Debugging with GDB)
---
::: header
Next: [libthread_db.so.1 file](libthread_005fdb_002eso_002e1-file.html#libthread_005fdb_002eso_002e1-file)]
:::

---

#### 22.8.1 Automatically loading init file in the current directory

By default, [GDB] reads and executes the canned sequences of commands from init file (if any) in the current working directory, see [Init File in the Current Directory during Startup](Initialization-Files.html#Init-File-in-the-Current-Directory-during-Startup).

Note that loading of this local `.gdbinit` file also requires accordingly configured `auto-load safe-path` (see [Auto-loading safe path](Auto_002dloading-safe-path.html#Auto_002dloading-safe-path)).

`set auto-load local-gdbinit [on|off]`

Enable or disable the auto-loading of canned sequences of commands (see [Sequences](Sequences.html#Sequences)) found in init file in the current directory.

`show auto-load local-gdbinit`

Show whether auto-loading of canned sequences of commands from init file in the current directory is enabled or disabled.

`info auto-load local-gdbinit`

Print whether canned sequences of commands from init file in the current directory have been auto-loaded.
