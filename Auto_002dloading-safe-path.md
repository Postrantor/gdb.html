---
description: Auto-loading safe path (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Auto-loading safe path (Debugging with GDB)
lang: en
resource-type: document
title: Auto-loading safe path (Debugging with GDB)
---
::: header
Next: [Auto-loading verbose mode](Auto_002dloading-verbose-mode.html#Auto_002dloading-verbose-mode)]
:::

---

#### 22.8.3 Security restriction for auto-loading

As the files of inferior can come from untrusted source (such as submitted by an application user) [GDB]' setting to list directories trusted for loading files not explicitly requested by user. Each directory can also be a shell wildcard pattern.

If the path is not set properly you will see a warning and the file will not get loaded:

::: smallexample

```bash
$ ./gdb -q ./gdb
Reading symbols from /home/user/gdb/gdb...
warning: File "/home/user/gdb/gdb-gdb.gdb" auto-loading has been
         declined by your `auto-load safe-path' set
         to "$debugdir:$datadir/auto-load".
warning: File "/home/user/gdb/gdb-gdb.py" auto-loading has been
         declined by your `auto-load safe-path' set
         to "$debugdir:$datadir/auto-load".
```

:::

To instruct [GDB] like this:

::: smallexample

```bash
$ gdb -q -iex "set auto-load safe-path /home/user/gdb" ./gdb
```

:::

The list of trusted directories is controlled by the following commands:

`set auto-load safe-path [directories]`

Set the list of directories (and their subdirectories) trusted for automatic loading and execution of scripts. You can also enter a specific trusted file. Each directory can also be a shell wildcard pattern; wildcards do not match directory separator - see `FNM_PATHNAME` for system function `fnmatch` (see [fnmatch](http://www.gnu.org/software/libc/manual/html_node/Wildcard-Matching.html#Wildcard-Matching) in GNU C Library Reference Manual). If you omit `directories` compilation.

The list of directories uses path separator ('`:`' on MS-Windows and MS-DOS) to separate directories, similarly to the `PATH` environment variable.

`show auto-load safe-path`

Show the list of directories trusted for automatic loading and execution of scripts.

`add-auto-load-safe-path`

Add an entry (or list of entries) to the list of directories trusted for automatic loading and execution of scripts. Multiple entries may be delimited by the host platform path separator in use.

This variable defaults to what `--with-auto-load-dir` has been configured to (see [with-auto-load-dir](objfile_002dgdbdotext-file.html#with_002dauto_002dload_002ddir)). `$debugdir`.

Setting this variable to `/`. This variable is supposed to be set to the system directories writable by the system superuser only. Users can add their source directories in init files in their home directories (see [Home Directory Init File](Initialization-Files.html#Home-Directory-Init-File)). See also deprecated init file in the current directory (see [Init File in the Current Directory during Startup](Initialization-Files.html#Init-File-in-the-Current-Directory-during-Startup)).

To force [GDB] to load the files it declined to load in the previous example, you could use one of the following ways:

`~/.gdbinit`'

:   Specify this trusted directory (or a file) as additional component of the list. You have to specify also any existing directories displayed by by '`show auto-load safe-path`' in this example).

[gdb -iex \"set auto-load safe-path /usr:/bin:\~/src/gdb\" ...]

:   Specify this directory as in the previous case but just for a single [GDB] session.

[gdb -iex \"set auto-load safe-path /\" ...]

:   Disable auto-loading safety for a single [GDB] session will come from trusted sources.

[./configure \--without-auto-load-safe-path]

:   During compilation of [GDB] come from trusted sources.

On the other hand you can also explicitly forbid automatic files loading which also suppresses any such warning messages:

[gdb -iex \"set auto-load no\" ...]

:   You can use [GDB] session.

`~/.gdbinit`'

:   Disable auto-loading globally for the user (see [Home Directory Init File](Initialization-Files.html#Home-Directory-Init-File)). While it is improbable, you could also use system init file instead (see [System-wide configuration](System_002dwide-configuration.html#System_002dwide-configuration)).

This setting applies to the file names as entered by user. If no entry matches [GDB] already canonicalizes most of the filenames on its own before starting the comparison so a canonical form of directories is recommended to be entered.

---

::: header
Next: [Auto-loading verbose mode](Auto_002dloading-verbose-mode.html#Auto_002dloading-verbose-mode)]
:::
