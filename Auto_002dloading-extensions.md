---
tip: translate by openai@2023-06-23 11:52:33
...
---
description: Auto-loading extensions (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Auto-loading extensions (Debugging with GDB)
lang: en
resource-type: document
title: Auto-loading extensions (Debugging with GDB)
---------------------------------------------------

::: header
Next: [Multiple Extension Languages](Multiple-Extension-Languages.html#Multiple-Extension-Languages)]
:::

---

### 23.5 Auto-loading extensions

[GDB] file](objfile_002dgdbdotext-file.html#objfile_002dgdbdotext-file)) and the `.debug_gdb_scripts` section of modern file formats like ELF (see [The `.debug_gdb_scripts` section](dotdebug_005fgdb_005fscripts-section.html#dotdebug_005fgdb_005fscripts-section)). For a discussion of the differences between these two approaches see [Which flavor to choose?](Which-flavor-to-choose_003f.html#Which-flavor-to-choose_003f).

> [GDB]文件（objfile_002dgdbdotext-file.html#objfile_002dgdbdotext-file）和现代文件格式（如 ELF）中的 `.debug_gdb_scripts` 部分（参见[` .debug_gdb_scripts` 部分](dotdebug_005fgdb_005fscripts-section.html#dotdebug_005fgdb_005fscripts-section)）。有关这两种方法之间的区别，请参见 [Which flavor to choose?](Which-flavor-to-choose_003f.html#Which-flavor-to-choose_003f)。

The auto-loading feature is useful for supplying application-specific debugging commands and features.

> 自动加载功能对于提供特定于应用的调试命令和功能很有用。

Auto-loading can be enabled or disabled, and the list of auto-loaded scripts can be printed. See the '`auto-loading` command files see [Auto-loading sequences](Auto_002dloading-sequences.html#Auto_002dloading-sequences). For Python files see [Python Auto-loading](Python-Auto_002dloading.html#Python-Auto_002dloading).

> 自动加载可以启用或禁用，并可以打印自动加载脚本的列表。请参阅'自动加载'命令文件，参见[自动加载序列](Auto_002dloading-sequences.html#Auto_002dloading-sequences)。关于 Python 文件，请参阅 [Python 自动加载](Python-Auto_002dloading.html#Python-Auto_002dloading)。

Note that loading of this script file also requires accordingly configured `auto-load safe-path` (see [Auto-loading safe path](Auto_002dloading-safe-path.html#Auto_002dloading-safe-path)).

---

• [objfile-gdbdotext file](objfile_002dgdbdotext-file.html#objfile_002dgdbdotext-file) file

> • [文件 objfile-gdbdotext](objfile_002dgdbdotext-file.html#objfile_002dgdbdotext-file)

• [dotdebug_gdb_scripts section](dotdebug_005fgdb_005fscripts-section.html#dotdebug_005fgdb_005fscripts-section):        The `.debug_gdb_scripts` section

> • [dotdebug_gdb_scripts 章节](dotdebug_005fgdb_005fscripts-section.html#dotdebug_005fgdb_005fscripts-section):         `.debug_gdb_scripts` 章节

• [Which flavor to choose?](Which-flavor-to-choose_003f.html#Which-flavor-to-choose_003f):                               Choosing between these approaches

> • [要选择哪种口味？](Which-flavor-to-choose_003f.html#Which-flavor-to-choose_003f): 保持选择这些方法之间的平衡。

---
