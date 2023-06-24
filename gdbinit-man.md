---
tip: translate by openai@2023-06-23 21:37:09
...
---
description: gdbinit man (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: gdbinit man (Debugging with GDB)
lang: en
resource-type: document
title: gdbinit man (Debugging with GDB)
---
::: header
Next: [gdb-add-index man](gdb_002dadd_002dindex-man.html#gdb_002dadd_002dindex-man)]
:::

---

#### gdbinit man

### gdbinit

::: format

```format

~/.config/gdb/gdbinit

~/.gdbinit

./.gdbinit
```

:::


These files contain [GDB] startup. The lines of contents are canned sequences of commands, described in [Sequences](Sequences.html#Sequences).

> 这些文件包含[GDB]启动。内容行是在[Sequences](Sequences.html#Sequences)中描述的命令序列。

Please read more in [Startup](Startup.html#Startup).

`(not enabled with --with-system-gdbinit` during compilation)


:   System-wide initialization file. It is executed unless user specified [GDB] option `-nx` or `-n`. See more in

> 系统级初始化文件。除非用户指定[GDB]选项`-nx`或`-n`，否则将执行该文件。更多信息请参见

`(not enabled with --with-system-gdbinit-dir` during compilation)


:   System-wide initialization directory. All files in this directory are executed on startup unless user specified [GDB] option `-nx` or `-n`, as long as they have a recognized file extension. See more in [System-wide configuration](System_002dwide-configuration.html#System_002dwide-configuration).

> 系统级初始化目录。只要文件具有可识别的文件扩展名，除非用户指定[GDB]选项“-nx”或“-n”，否则在启动时将执行此目录中的所有文件。有关详细信息，请参阅[系统级配置](System_002dwide-configuration.html#System_002dwide-configuration)。

`~/.config/gdb/gdbinit or ~/.gdbinit`


:   User initialization file. It is executed unless user specified [GDB] options `-nx`, `-n` or `-nh`.

> 用户初始化文件。除非用户指定[GDB]选项“-nx”、“-n”或“-nh”，否则将执行此文件。

`.gdbinit`


:   Initialization file for current directory. It may need to be enabled with [GDB] security command `set auto-load local-gdbinit`. See more in [Init File in the Current Directory](Init-File-in-the-Current-Directory.html#Init-File-in-the-Current-Directory).

> 这是当前目录的初始化文件。可能需要使用[GDB]安全命令“set auto-load local-gdbinit”来启用它。更多信息请参阅[当前目录的初始化文件](Init-File-in-the-Current-Directory.html#Init-File-in-the-Current-Directory)。
