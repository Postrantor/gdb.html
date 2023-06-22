---
description: objfile-gdbdotext file (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: objfile-gdbdotext file (Debugging with GDB)
lang: en
resource-type: document
title: objfile-gdbdotext file (Debugging with GDB)
---
::: header
Next: [dotdebug_gdb_scripts section](dotdebug_005fgdb_005fscripts-section.html#dotdebug_005fgdb_005fscripts-section)]
:::

---

#### 23.5.1 The `objfile-gdb.ext`

When a new object file is read, [GDB] is the file extension for the extension language:

`objfile-gdb.gdb`

:   GDB's own command language

`objfile-gdb.py`

:   Python

`objfile-gdb.scm`

:   Guile

`script-name` will evaluate it as a script in the specified extension language.

If this file does not exist, then [GDB], because Windows filesystems disallow colons in file names.)

Note that loading of these files requires an accordingly configured `auto-load safe-path` (see [Auto-loading safe path](Auto_002dloading-safe-path.html#Auto_002dloading-safe-path)).

For object files using `.exe` stripping is case insensitive and it is attempted on any platform. This makes the script filenames compatible between Unix and MS-Windows hosts.

`set auto-load scripts-directory [directories]`

Control [GDB]' on MS-Windows and MS-DOS).

Each entry here needs to be covered also by the security setting `set auto-load safe-path` (see [set auto-load safe-path](Auto_002dloading-safe-path.html#set-auto_002dload-safe_002dpath)).

This variable defaults to `$debugdir:$datadir/auto-load`.

Any reference to `$debugdir` directory separators, depending on the host platform.

The list of directories uses path separator ('`:`' on MS-Windows and MS-DOS) to separate directories, similarly to the `PATH` environment variable.

`show auto-load scripts-directory`

Show [GDB] auto-loaded scripts location.

`add-auto-load-scripts-directory [directories…]`

Add an entry (or list of entries) to the list of auto-loaded scripts locations. Multiple entries may be delimited by the host platform path separator in use.

[GDB] file should be careful to avoid errors if it is evaluated more than once.

---

::: header
Next: [dotdebug_gdb_scripts section](dotdebug_005fgdb_005fscripts-section.html#dotdebug_005fgdb_005fscripts-section)]
:::
