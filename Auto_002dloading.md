---
tip: translate by openai@2023-06-23 17:47:14
...
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

> GDB可以满足您的项目需求，但有时可能会产生意外的结果或引入安全风险（例如，如果文件来自不可信的来源）。


There are various kinds of files [GDB] supports auto-loading code written in various extension languages. See [Auto-loading extensions](Auto_002dloading-extensions.html#Auto_002dloading-extensions).

> GDB 支持自动加载用各种扩展语言编写的代码，有多种类型的文件。请参阅[自动加载扩展](Auto_002dloading-extensions.html#Auto_002dloading-extensions)。

Note that loading of these associated files (including the local `.gdbinit` file) requires accordingly configured `auto-load safe-path` (see [Auto-loading safe path](Auto_002dloading-safe-path.html#Auto_002dloading-safe-path)).


For these reasons, [GDB] includes commands and options to let you control when to auto-load files and which files should be auto-loaded.

> 因此，[GDB]包含了命令和选项，让你控制何时自动加载文件以及哪些文件应该被自动加载。

`set auto-load off`


Globally disable loading of all auto-loaded files. You may want to use this command with the '`-iex`' option (see [Option -init-eval-command](Startup.html#Option-_002dinit_002deval_002dcommand)) such as:

> 全局禁用加载所有自动加载的文件。您可能希望使用带有“-iex”选项的此命令（请参阅[Option -init-eval-command](Startup.html#Option-_002dinit_002deval_002dcommand))，例如：

::: smallexample

```bash
$ gdb -iex "set auto-load off" untrusted-executable corefile
```

:::


Be aware that system init file (see [System-wide configuration](System_002dwide-configuration.html#System_002dwide-configuration)) and init files from your home directory (see [Home Directory Init File](Initialization-Files.html#Home-Directory-Init-File)) still get read (as they come from generally trusted directories). To prevent [GDB] option (see [Mode Options](Mode-Options.html#Mode-Options)), in addition to `set auto-load no`.

> 要注意，系统初始文件（参见[系统范围配置](System_002dwide-configuration.html#System_002dwide-configuration))和来自您主目录的初始文件（参见[主目录初始文件](Initialization-Files.html#Home-Directory-Init-File))仍然会被读取（因为它们来自一般可信的目录）。除了`set auto-load no`外，还可以防止[GDB]选项（参见[模式选项](Mode-Options.html#Mode-Options)）。

`show auto-load`


Show whether auto-loading of each specific '`auto-load`' file(s) is enabled or disabled.

> 显示每个特定'自动加载'文件的自动加载是否启用或禁用。

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

> 打印每个特定的'自动加载'文件是否已自动加载。

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

> 这些是[GDB]自动加载的控制命令：

---


See [set auto-load off](#set-auto_002dload-off).                                                                          Disable auto-loading globally.

> 查看[关闭自动加载](#set-auto_002dload-off)。全局禁用自动加载。

See [show auto-load](#show-auto_002dload).                                                                                Show setting of all kinds of files.

> 请参见[显示自动加载](#show-auto_002dload)。显示所有类型文件的设置。

See [info auto-load](#info-auto_002dload).                                                                                Show state of all kinds of files.

> 请参见[自动加载信息](#info-auto_002dload)。显示所有类型文件的状态。

See [set auto-load gdb-scripts](Auto_002dloading-sequences.html#set-auto_002dload-gdb_002dscripts).                       Control for [GDB] command scripts.

> 请参阅[设置自动加载GDB脚本](Auto_002dloading-sequences.html#set-auto_002dload-gdb_002dscripts)。控制[GDB]命令脚本。

See [show auto-load gdb-scripts](Auto_002dloading-sequences.html#show-auto_002dload-gdb_002dscripts).                     Show setting of [GDB] command scripts.

> 请参阅[显示自动加载GDB脚本](Auto_002dloading-sequences.html#show-auto_002dload-gdb_002dscripts)。显示[GDB]命令脚本的设置。

See [info auto-load gdb-scripts](Auto_002dloading-sequences.html#info-auto_002dload-gdb_002dscripts).                     Show state of [GDB] command scripts.

> 请参阅[自动加载GDB脚本的信息](Auto_002dloading-sequences.html#info-auto_002dload-gdb_002dscripts)。显示GDB命令脚本的状态。

See [set auto-load python-scripts](Python-Auto_002dloading.html#set-auto_002dload-python_002dscripts).                    Control for [GDB] Python scripts.

> 请参阅[设置自动加载Python脚本](Python-Auto_002dloading.html#set-auto_002dload-python_002dscripts)。控制[GDB] Python脚本。

See [show auto-load python-scripts](Python-Auto_002dloading.html#show-auto_002dload-python_002dscripts).                  Show setting of [GDB] Python scripts.

> 看看[显示自动加载的Python脚本](Python-Auto_002dloading.html#show-auto_002dload-python_002dscripts)。显示[GDB] Python脚本的设置。

See [info auto-load python-scripts](Python-Auto_002dloading.html#info-auto_002dload-python_002dscripts).                  Show state of [GDB] Python scripts.

> 请参阅[自动加载Python脚本的信息](Python-Auto_002dloading.html#info-auto_002dload-python_002dscripts)。显示[GDB] Python脚本的状态。

See [set auto-load guile-scripts](Guile-Auto_002dloading.html#set-auto_002dload-guile_002dscripts).                       Control for [GDB] Guile scripts.

> 请参阅[设置自动加载Guile脚本](Guile-Auto_002dloading.html#set-auto_002dload-guile_002dscripts)。控制[GDB] Guile脚本。

See [show auto-load guile-scripts](Guile-Auto_002dloading.html#show-auto_002dload-guile_002dscripts).                     Show setting of [GDB] Guile scripts.

> 请参见[显示自动加载Guile脚本](Guile-Auto_002dloading.html#show-auto_002dload-guile_002dscripts)。显示GDB Guile脚本的设置。

See [info auto-load guile-scripts](Guile-Auto_002dloading.html#info-auto_002dload-guile_002dscripts).                     Show state of [GDB] Guile scripts.

> 请参阅[info auto-load guile-scripts](Guile-Auto_002dloading.html#info-auto_002dload-guile_002dscripts)。显示[GDB] Guile脚本的状态。

See [set auto-load scripts-directory](objfile_002dgdbdotext-file.html#set-auto_002dload-scripts_002ddirectory).           Control for [GDB] auto-loaded scripts location.

> 请参考[设置自动加载脚本目录](objfile_002dgdbdotext-file.html#set-auto_002dload-scripts_002ddirectory)。控制[GDB]自动加载脚本的位置。

See [show auto-load scripts-directory](objfile_002dgdbdotext-file.html#show-auto_002dload-scripts_002ddirectory).         Show [GDB] auto-loaded scripts location.

> 查看[显示自动加载脚本目录](objfile_002dgdbdotext-file.html#show-auto_002dload-scripts_002ddirectory)。显示[GDB]自动加载脚本的位置。

See [add-auto-load-scripts-directory](objfile_002dgdbdotext-file.html#add_002dauto_002dload_002dscripts_002ddirectory).   Add directory for auto-loaded scripts location list.

> 请参阅[add-auto-load-scripts-directory](objfile_002dgdbdotext-file.html#add_002dauto_002dload_002dscripts_002ddirectory)。 为自动加载脚本位置列表添加目录。

See [set auto-load local-gdbinit](Init-File-in-the-Current-Directory.html#set-auto_002dload-local_002dgdbinit).           Control for init file in the current directory.

> 请参阅[设置auto-load local-gdbinit](Init-File-in-the-Current-Directory.html#set-auto_002dload-local_002dgdbinit)。控制当前目录中的初始文件。

See [show auto-load local-gdbinit](Init-File-in-the-Current-Directory.html#show-auto_002dload-local_002dgdbinit).         Show setting of init file in the current directory.

> 请参阅[显示自动加载的本地GDBINIT](Init-File-in-the-Current-Directory.html#show-auto_002dload-local_002dgdbinit)。显示当前目录中的初始文件设置。

See [info auto-load local-gdbinit](Init-File-in-the-Current-Directory.html#info-auto_002dload-local_002dgdbinit).         Show state of init file in the current directory.

> 请参阅[info auto-load local-gdbinit](Init-File-in-the-Current-Directory.html#info-auto_002dload-local_002dgdbinit)。显示当前目录中的初始文件状态。

See [set auto-load libthread-db](libthread_005fdb_002eso_002e1-file.html#set-auto_002dload-libthread_002ddb).             Control for thread debugging library.

> 请参阅[设置自动加载libthread-db](libthread_005fdb_002eso_002e1-file.html#set-auto_002dload-libthread_002ddb)。控制线程调试库。

See [show auto-load libthread-db](libthread_005fdb_002eso_002e1-file.html#show-auto_002dload-libthread_002ddb).           Show setting of thread debugging library.

> 请参阅[显示自动加载 libthread-db](libthread_005fdb_002eso_002e1-file.html#show-auto_002dload-libthread_002ddb)。显示线程调试库的设置。

See [info auto-load libthread-db](libthread_005fdb_002eso_002e1-file.html#info-auto_002dload-libthread_002ddb).           Show state of thread debugging library.

> 请参阅[libthread-db自动加载信息](libthread_005fdb_002eso_002e1-file.html#info-auto_002dload-libthread_002ddb)。显示线程调试库的状态。

See [set auto-load safe-path](Auto_002dloading-safe-path.html#set-auto_002dload-safe_002dpath).                           Control directories trusted for automatic loading.

> 请参阅[设置自动加载安全路径](Auto_002dloading-safe-path.html#set-auto_002dload-safe_002dpath)。控制信任自动加载的目录。

See [show auto-load safe-path](Auto_002dloading-safe-path.html#show-auto_002dload-safe_002dpath).                         Show directories trusted for automatic loading.

> 请参见[显示自动加载安全路径](Auto_002dloading-safe-path.html#show-auto_002dload-safe_002dpath)。显示可信任的自动加载目录。

See [add-auto-load-safe-path](Auto_002dloading-safe-path.html#add_002dauto_002dload_002dsafe_002dpath).                   Add directory trusted for automatic loading.

> 请参阅[add-auto-load-safe-path](Auto_002dloading-safe-path.html#add_002dauto_002dload_002dsafe_002dpath)。添加可信任的目录以进行自动加载。

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
