---
tip: translate by openai@2023-06-23 23:27:03
...
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

> 默认情况下，GDB会从当前工作目录中的初始文件（如果有的话）中读取和执行命令序列，参见[启动时当前目录中的初始文件](Initialization-Files.html#Init-File-in-the-Current-Directory-during-Startup)。


Note that loading of this local `.gdbinit` file also requires accordingly configured `auto-load safe-path` (see [Auto-loading safe path](Auto_002dloading-safe-path.html#Auto_002dloading-safe-path)).

> 注意，加载这个本地`.gdbinit`文件也需要相应配置的`auto-load safe-path`（参见[自动加载安全路径](Auto_002dloading-safe-path.html#Auto_002dloading-safe-path)）。

`set auto-load local-gdbinit [on|off]`


Enable or disable the auto-loading of canned sequences of commands (see [Sequences](Sequences.html#Sequences)) found in init file in the current directory.

> 启用或禁用当前目录中的初始文件中发现的命令序列的自动加载（参见[序列](Sequences.html#Sequences)）。

`show auto-load local-gdbinit`


Show whether auto-loading of canned sequences of commands from init file in the current directory is enabled or disabled.

> 检查当前目录中的初始文件是否启用了自动加载罐装命令序列的功能。

`info auto-load local-gdbinit`


Print whether canned sequences of commands from init file in the current directory have been auto-loaded.

> 打印当前目录中的初始文件中的罐装命令序列是否已自动加载。
