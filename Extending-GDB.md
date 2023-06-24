---
tip: translate by openai@2023-06-23 20:59:53
...
---
description: Extending GDB (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Extending GDB (Debugging with GDB)
lang: en
resource-type: document
title: Extending GDB (Debugging with GDB)
---
::: header
Next: [Interpreters](Interpreters.html#Interpreters)]
:::

---

## 23 Extending [GDB]

[GDB] for the program being debugged.


To facilitate the use of extension languages, [GDB] Command Files. See [Command files](Command-Files.html#Command-Files).

> 为了方便使用扩展语言，[GDB] 命令文件。参见[命令文件](Command-Files.html#Command-Files)。


You can control how [GDB] evaluates these files with the following setting:

> 你可以通过以下设置来控制GDB如何评估这些文件：

`set script-extension off`

All scripts are always evaluated as [GDB] Command Files.

`set script-extension soft`


The debugger determines the scripting language based on filename extension. If this scripting language is supported, [GDB] Command File.

> 调试器根据文件名后缀确定脚本语言。如果这种脚本语言受支持，[GDB]命令文件。

`set script-extension strict`


The debugger determines the scripting language based on filename extension, and evaluates the script using that language. If the language is not supported, then the evaluation fails.

> 调试器根据文件名的扩展名来确定脚本语言，并使用该语言来评估脚本。如果语言不受支持，则评估失败。

`show script-extension`

Display the current value of the `script-extension` option.

---

• [Sequences](Sequences.html#Sequences) Commands

• [Aliases](Aliases.html#Aliases):                                                                       Command Aliases

> • [别名](Aliases.html#Aliases)：命令别名
• [Python](Python.html#Python) using Python
• [Guile](Guile.html#Guile) using Guile

• [Auto-loading extensions](Auto_002dloading-extensions.html#Auto_002dloading-extensions):               Automatically loading extensions

> • [自动加载扩展](Auto_002dloading-extensions.html#Auto_002dloading-extensions):               自动加载扩展

• [Multiple Extension Languages](Multiple-Extension-Languages.html#Multiple-Extension-Languages):        Working with multiple extension languages

> • [多种扩展语言](Multiple-Extension-Languages.html#Multiple-Extension-Languages):      使用多种扩展语言进行工作

---

---

::: header
Next: [Interpreters](Interpreters.html#Interpreters)]
:::
