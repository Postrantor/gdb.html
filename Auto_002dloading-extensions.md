---
description: Auto-loading extensions (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Auto-loading extensions (Debugging with GDB)
lang: en
resource-type: document
title: Auto-loading extensions (Debugging with GDB)
---
::: header
Next: [Multiple Extension Languages](Multiple-Extension-Languages.html#Multiple-Extension-Languages)]
:::

---

### 23.5 Auto-loading extensions

[GDB] file](objfile_002dgdbdotext-file.html#objfile_002dgdbdotext-file)) and the `.debug_gdb_scripts` section of modern file formats like ELF (see [The `.debug_gdb_scripts` section](dotdebug_005fgdb_005fscripts-section.html#dotdebug_005fgdb_005fscripts-section)). For a discussion of the differences between these two approaches see [Which flavor to choose?](Which-flavor-to-choose_003f.html#Which-flavor-to-choose_003f).

The auto-loading feature is useful for supplying application-specific debugging commands and features.

Auto-loading can be enabled or disabled, and the list of auto-loaded scripts can be printed. See the '`auto-loading` command files see [Auto-loading sequences](Auto_002dloading-sequences.html#Auto_002dloading-sequences). For Python files see [Python Auto-loading](Python-Auto_002dloading.html#Python-Auto_002dloading).

Note that loading of this script file also requires accordingly configured `auto-load safe-path` (see [Auto-loading safe path](Auto_002dloading-safe-path.html#Auto_002dloading-safe-path)).

---

• [objfile-gdbdotext file](objfile_002dgdbdotext-file.html#objfile_002dgdbdotext-file) file
• [dotdebug_gdb_scripts section](dotdebug_005fgdb_005fscripts-section.html#dotdebug_005fgdb_005fscripts-section):        The `.debug_gdb_scripts` section
• [Which flavor to choose?](Which-flavor-to-choose_003f.html#Which-flavor-to-choose_003f):                               Choosing between these approaches

---
