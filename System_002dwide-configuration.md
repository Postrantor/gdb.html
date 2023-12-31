---
tip: translate by openai@2023-06-24 11:01:08
...
---
description: System-wide configuration (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: System-wide configuration (Debugging with GDB)
lang: en
resource-type: document
title: System-wide configuration (Debugging with GDB)
---
::: header
Previous: [Configure Options](Configure-Options.html#Configure-Options)]
:::

---

### C.6 System-wide configuration and settings

[GDB] does during startup](Startup.html#Startup)).

Here are the corresponding configure options:

`--with-system-gdbinit=file`


:   Specify that the default location of the system-wide init file is `file`.

> 指定系统默认的初始文件位置为'文件'。

`--with-system-gdbinit-dir=directory`


:   Specify that the default location of the system-wide init file directory is `directory`.

> 指定系统默认的初始文件目录位于“directory”。

If [GDB], they may be subject to relocation. Two possible cases:

- If the default location of this init file/directory contains `$prefix`.

- By contrast, if the default location does not contain the prefix, it will not be relocated. E.g. if [GDB] is installed.

> 相反，如果默认位置不包含前缀，它将不会被重新定位。例如，如果[GDB]已安装。


If the configured location of the system-wide init file (as given by the `--with-system-gdbinit` has started with the `set data-directory` command, the file will not be reread.

> 如果系统级初始文件（由`--with-system-gdbinit`提供的配置位置）以`set data-directory`命令开始，则该文件将不会被重新读取。


This applies similarly to the system-wide directory specified in `--with-system-gdbinit-dir`.

> 这同样适用于在`--with-system-gdbinit-dir`中指定的系统级目录。


Any supported scripting language can be used for these init files, as long as the file extension matches the scripting language. To be interpreted as regular [GDB] extension.

> 任何受支持的脚本语言都可以用于这些初始文件，只要文件扩展名与脚本语言匹配即可。要被解释为常规[GDB]扩展。

---


• [System-wide Configuration Scripts](System_002dwide-Configuration-Scripts.html#System_002dwide-Configuration-Scripts):        Installed System-wide Configuration Scripts

> • [系统级配置脚本](System_002dwide-Configuration-Scripts.html#System_002dwide-Configuration-Scripts):     已安装的系统级配置脚本

---

---

::: header
Previous: [Configure Options](Configure-Options.html#Configure-Options)]
:::
