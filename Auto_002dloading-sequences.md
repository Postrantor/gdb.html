---
tip: translate by openai@2023-06-23 17:46:04
...
---
description: Auto-loading sequences (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Auto-loading sequences (Debugging with GDB)
lang: en
resource-type: document
title: Auto-loading sequences (Debugging with GDB)
---
::: header
Previous: [Output](Output.html#Output)]
:::

---

#### 23.1.5 Controlling auto-loading native [GDB]


When a new object file is read (for example, due to the `file` command, or because the inferior has loaded a shared library), [GDB]. See [Auto-loading extensions](Auto_002dloading-extensions.html#Auto_002dloading-extensions).

> 当读取一个新的对象文件时（例如，由于`file`命令，或因为次级已加载了一个共享库），[GDB] 将会自动加载扩展。请参阅[自动加载扩展](Auto_002dloading-extensions.html#Auto_002dloading-extensions)。


Auto-loading can be enabled or disabled, and the list of auto-loaded scripts can be printed.

> 自动加载可以启用或禁用，可以打印自动加载脚本的列表。

`set auto-load gdb-scripts [on|off]`


Enable or disable the auto-loading of canned sequences of commands scripts.

> 启用或禁用自动加载命令脚本序列的罐头。

`show auto-load gdb-scripts`


Show whether auto-loading of canned sequences of commands scripts is enabled or disabled.

> 显示自动加载命令脚本序列是否已启用或禁用。

`info auto-load gdb-scripts [regexp]`


Print the list of all canned sequences of commands scripts that [GDB] auto-loaded.

> 打印GDB自动加载的所有罐装命令脚本的列表。


If `regexp` is supplied only canned sequences of commands scripts with matching names are printed.

> 如果提供了`regexp`，只会打印具有匹配名称的罐头序列命令脚本。
