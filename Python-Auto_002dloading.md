---
tip: translate by openai@2023-06-24 01:39:20
...
---
description: Python Auto-loading (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Python Auto-loading (Debugging with GDB)
lang: en
resource-type: document
title: Python Auto-loading (Debugging with GDB)
---
::: header
Next: [Python modules](Python-modules.html#Python-modules)]
:::

---

#### 23.3.3 Python Auto-loading


When a new object file is read (for example, due to the `file` command, or because the inferior has loaded a shared library), [GDB] and `.debug_gdb_scripts` section. See [Auto-loading extensions](Auto_002dloading-extensions.html#Auto_002dloading-extensions).

> 当读取一个新的对象文件时（例如，由于`file`命令，或者因为下级已加载了一个共享库），[GDB]会检查`.debug_gdb_scripts`部分。请参阅[自动加载扩展](Auto_002dloading-extensions.html#Auto_002dloading-extensions)。


The auto-loading feature is useful for supplying application-specific debugging commands and scripts.

> 自动加载功能对于提供特定应用程序的调试命令和脚本很有用。


Auto-loading can be enabled or disabled, and the list of auto-loaded scripts can be printed.

> 自动加载可以启用或禁用，可以打印自动加载脚本的列表。

`set auto-load python-scripts [on|off]`

Enable or disable the auto-loading of Python scripts.

`show auto-load python-scripts`

Show whether auto-loading of Python scripts is enabled or disabled.

`info auto-load python-scripts [regexp]`

Print the list of all Python scripts that [GDB] auto-loaded.


Also printed is the list of Python scripts that were mentioned in the `.debug_gdb_scripts` section and were either not found (see [dotdebug_gdb_scripts section](dotdebug_005fgdb_005fscripts-section.html#dotdebug_005fgdb_005fscripts-section)) or were not auto-loaded due to `auto-load safe-path` rejection (see [Auto-loading](Auto_002dloading.html#Auto_002dloading)). This is useful because their names are not printed when [GDB] tries to load them and fails. There may be many of them, and printing an error message for each one is problematic.

> 也打印出了在` .debug_gdb_scripts`部分中提到的Python脚本的列表，这些脚本要么没有找到（参见[dotdebug_gdb_scripts section](dotdebug_005fgdb_005fscripts-section.html#dotdebug_005fgdb_005fscripts-section))，要么由于`auto-load safe-path`拒绝而没有自动加载（参见[Auto-loading](Auto_002dloading.html#Auto_002dloading))。这是有用的，因为当[GDB]尝试加载它们而失败时，它们的名字不会被打印出来。它们可能有很多，为每个脚本打印一个错误消息是有问题的。


If `regexp` is supplied only Python scripts with matching names are printed.

> 如果提供了`regexp`，只会打印出名称匹配的Python脚本。

Example:

::: smallexample

```bash
(gdb) info auto-load python-scripts
Loaded Script
Yes    py-section-script.py
       full name: /tmp/py-section-script.py
No     my-foo-pretty-printers.py
```

:::


When reading an auto-loaded file or script, [GDB] sets the *current objfile*. This is available via the `gdb.current_objfile` function (see [Objfiles In Python](Objfiles-In-Python.html#Objfiles-In-Python)). This can be useful for registering objfile-specific pretty-printers and frame-filters.

> 当读取自动加载的文件或脚本时，[GDB]设置*当前objfile*。这可以通过`gdb.current_objfile`函数获得（参见[Python中的Objfiles](Objfiles-In-Python.html#Objfiles-In-Python)）。这可以用于注册objfile特定的pretty-printers和frame-filters。

---

::: header
Next: [Python modules](Python-modules.html#Python-modules)]
:::
