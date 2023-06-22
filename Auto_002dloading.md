---
description: Auto-loading (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Auto-loading (Debugging with GDB)
lang: en
resource-type: document
title: Auto-loading (Debugging with GDB)
---
::: header
Next: [Messages/Warnings](Messages_002fWarnings.html#Messages_002fWarnings)]
:::

---

### 22.8 Automatically loading associated files

[GDB] to the needs of your project, it can sometimes produce unexpected results or introduce security risks (e.g., if the file comes from untrusted sources).

There are various kinds of files [GDB] supports auto-loading code written in various extension languages. See [Auto-loading extensions](Auto_002dloading-extensions.html#Auto_002dloading-extensions).

Note that loading of these associated files (including the local `.gdbinit` file) requires accordingly configured `auto-load safe-path` (see [Auto-loading safe path](Auto_002dloading-safe-path.html#Auto_002dloading-safe-path)).

For these reasons, [GDB] includes commands and options to let you control when to auto-load files and which files should be auto-loaded.

`set auto-load off`

Globally disable loading of all auto-loaded files. You may want to use this command with the '`-iex`' option (see [Option -init-eval-command](Startup.html#Option-_002dinit_002deval_002dcommand)) such as:

::: smallexample

```bash
$ gdb -iex "set auto-load off" untrusted-executable corefile
```

:::

Be aware that system init file (see [System-wide configuration](System_002dwide-configuration.html#System_002dwide-configuration)) and init files from your home directory (see [Home Directory Init File](Initialization-Files.html#Home-Directory-Init-File)) still get read (as they come from generally trusted directories). To prevent [GDB] option (see [Mode Options](Mode-Options.html#Mode-Options)), in addition to `set auto-load no`.

`show auto-load`

Show whether auto-loading of each specific '`auto-load`' file(s) is enabled or disabled.

::: smallexample

```bash
(gdb) show auto-load
gdb-scripts:  Auto-loading of canned sequences of commands scripts is on.
libthread-db:  Auto-loading of inferior specific libthread_db is on.
local-gdbinit:  Auto-loading of .gdbinit script from current directory
                is on.
python-scripts:  Auto-loading of Python scripts is on.
safe-path:  List of directories from which it is safe to auto-load files
            is $debugdir:$datadir/auto-load.
scripts-directory:  List of directories from which to load auto-loaded scripts
                    is $debugdir:$datadir/auto-load.
```

:::

`info auto-load`

Print whether each specific '`auto-load`' file(s) have been auto-loaded or not.

::: smallexample

```bash
(gdb) info auto-load
gdb-scripts:
Loaded  Script
Yes     /home/user/gdb/gdb-gdb.gdb
libthread-db:  No auto-loaded libthread-db.
local-gdbinit:  Local .gdbinit file "/home/user/gdb/.gdbinit" has been
                loaded.
python-scripts:
Loaded  Script
Yes     /home/user/gdb/gdb-gdb.py
```

:::

These are [GDB] control commands for the auto-loading:

---

See [set auto-load off](#set-auto_002dload-off).                                                                          Disable auto-loading globally.
See [show auto-load](#show-auto_002dload).                                                                                Show setting of all kinds of files.
See [info auto-load](#info-auto_002dload).                                                                                Show state of all kinds of files.
See [set auto-load gdb-scripts](Auto_002dloading-sequences.html#set-auto_002dload-gdb_002dscripts).                       Control for [GDB] command scripts.
See [show auto-load gdb-scripts](Auto_002dloading-sequences.html#show-auto_002dload-gdb_002dscripts).                     Show setting of [GDB] command scripts.
See [info auto-load gdb-scripts](Auto_002dloading-sequences.html#info-auto_002dload-gdb_002dscripts).                     Show state of [GDB] command scripts.
See [set auto-load python-scripts](Python-Auto_002dloading.html#set-auto_002dload-python_002dscripts).                    Control for [GDB] Python scripts.
See [show auto-load python-scripts](Python-Auto_002dloading.html#show-auto_002dload-python_002dscripts).                  Show setting of [GDB] Python scripts.
See [info auto-load python-scripts](Python-Auto_002dloading.html#info-auto_002dload-python_002dscripts).                  Show state of [GDB] Python scripts.
See [set auto-load guile-scripts](Guile-Auto_002dloading.html#set-auto_002dload-guile_002dscripts).                       Control for [GDB] Guile scripts.
See [show auto-load guile-scripts](Guile-Auto_002dloading.html#show-auto_002dload-guile_002dscripts).                     Show setting of [GDB] Guile scripts.
See [info auto-load guile-scripts](Guile-Auto_002dloading.html#info-auto_002dload-guile_002dscripts).                     Show state of [GDB] Guile scripts.
See [set auto-load scripts-directory](objfile_002dgdbdotext-file.html#set-auto_002dload-scripts_002ddirectory).           Control for [GDB] auto-loaded scripts location.
See [show auto-load scripts-directory](objfile_002dgdbdotext-file.html#show-auto_002dload-scripts_002ddirectory).         Show [GDB] auto-loaded scripts location.
See [add-auto-load-scripts-directory](objfile_002dgdbdotext-file.html#add_002dauto_002dload_002dscripts_002ddirectory).   Add directory for auto-loaded scripts location list.
See [set auto-load local-gdbinit](Init-File-in-the-Current-Directory.html#set-auto_002dload-local_002dgdbinit).           Control for init file in the current directory.
See [show auto-load local-gdbinit](Init-File-in-the-Current-Directory.html#show-auto_002dload-local_002dgdbinit).         Show setting of init file in the current directory.
See [info auto-load local-gdbinit](Init-File-in-the-Current-Directory.html#info-auto_002dload-local_002dgdbinit).         Show state of init file in the current directory.
See [set auto-load libthread-db](libthread_005fdb_002eso_002e1-file.html#set-auto_002dload-libthread_002ddb).             Control for thread debugging library.
See [show auto-load libthread-db](libthread_005fdb_002eso_002e1-file.html#show-auto_002dload-libthread_002ddb).           Show setting of thread debugging library.
See [info auto-load libthread-db](libthread_005fdb_002eso_002e1-file.html#info-auto_002dload-libthread_002ddb).           Show state of thread debugging library.
See [set auto-load safe-path](Auto_002dloading-safe-path.html#set-auto_002dload-safe_002dpath).                           Control directories trusted for automatic loading.
See [show auto-load safe-path](Auto_002dloading-safe-path.html#show-auto_002dload-safe_002dpath).                         Show directories trusted for automatic loading.
See [add-auto-load-safe-path](Auto_002dloading-safe-path.html#add_002dauto_002dload_002dsafe_002dpath).                   Add directory trusted for automatic loading.

---

+:-----------------------------------------------------------------------------------------------------------------------------------+-----------------------+:---------------------------------------------------+
| • [Init File in the Current Directory](Init-File-in-the-Current-Directory.html#Init-File-in-the-Current-Directory)' |
+------------------------------------------------------------------------------------------------------------------------------------+-----------------------+----------------------------------------------------+
| • [libthread_db.so.1 file](libthread_005fdb_002eso_002e1-file.html#libthread_005fdb_002eso_002e1-file)'  |
+------------------------------------------------------------------------------------------------------------------------------------+-----------------------+----------------------------------------------------+
| ``menu-comment                                                                                                                   |                       |                                                    | |``                                                                                                                                |                       |                                                    |
+------------------------------------------------------------------------------------------------------------------------------------+-----------------------+----------------------------------------------------+
| • [Auto-loading safe path](Auto_002dloading-safe-path.html#Auto_002dloading-safe-path)'     |
+------------------------------------------------------------------------------------------------------------------------------------+-----------------------+----------------------------------------------------+
| • [Auto-loading verbose mode](Auto_002dloading-verbose-mode.html#Auto_002dloading-verbose-mode)'              |
+------------------------------------------------------------------------------------------------------------------------------------+-----------------------+----------------------------------------------------+

---

::: header
Next: [Messages/Warnings](Messages_002fWarnings.html#Messages_002fWarnings)]
:::
