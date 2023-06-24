---
tip: translate by openai@2023-06-23 23:00:12
...
---
description: Guile Auto-loading (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Guile Auto-loading (Debugging with GDB)
lang: en
resource-type: document
title: Guile Auto-loading (Debugging with GDB)
---
::: header
Next: [Guile Modules](Guile-Modules.html#Guile-Modules)]
:::

---

#### 23.4.4 Guile Auto-loading


When a new object file is read (for example, due to the `file` command, or because the inferior has loaded a shared library), [GDB] and the `.debug_gdb_scripts` section. See [Auto-loading extensions](Auto_002dloading-extensions.html#Auto_002dloading-extensions).

> 当一个新的对象文件被读取（例如，由于`file`命令或因为次级程序已经加载了一个共享库），GDB会检查`.debug_gdb_scripts`部分。参见[自动加载扩展](Auto_002dloading-extensions.html#Auto_002dloading-extensions)。


The auto-loading feature is useful for supplying application-specific debugging commands and scripts.

> 自动加载功能对于提供应用程序特定的调试命令和脚本很有用。


Auto-loading can be enabled or disabled, and the list of auto-loaded scripts can be printed.

> 自动加载可以启用或禁用，并且可以打印出自动加载脚本的列表。

`set auto-load guile-scripts [on|off]`

Enable or disable the auto-loading of Guile scripts.

`show auto-load guile-scripts`

Show whether auto-loading of Guile scripts is enabled or disabled.

`info auto-load guile-scripts [regexp]`

Print the list of all Guile scripts that [GDB] auto-loaded.


Also printed is the list of Guile scripts that were mentioned in the `.debug_gdb_scripts` section and were not found. This is useful because their names are not printed when [GDB] tries to load them and fails. There may be many of them, and printing an error message for each one is problematic.

> 此外，还会打印出在`.debug_gdb_scripts`部分提到的但没有找到的Guile脚本的列表。这很有用，因为当[GDB]尝试加载它们失败时，它们的名字不会被打印出来。它们可能有很多，并且为每一个打印一个错误消息是有问题的。


If `regexp` is supplied only Guile scripts with matching names are printed.

> 如果提供了`regexp`，只会打印出名称匹配的Guile脚本。

Example:

::: smallexample

```bash
(gdb) info auto-load guile-scripts
Loaded Script
Yes    scm-section-script.scm
       full name: /tmp/scm-section-script.scm
No     my-foo-pretty-printers.scm
```

:::


When reading an auto-loaded file, [GDB] sets the *current objfile*. This is available via the `current-objfile` procedure (see [Objfiles In Guile](Objfiles-In-Guile.html#Objfiles-In-Guile)). This can be useful for registering objfile-specific pretty-printers.

> 当读取自动加载的文件时，[GDB]会设置*当前 objfile*。可以通过`current-objfile`过程获取（参见[Guile中的Objfiles](Objfiles-In-Guile.html#Objfiles-In-Guile)）。这可以用于注册objfile特定的pretty-printers。
