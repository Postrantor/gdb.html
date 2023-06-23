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

You can control how [GDB] evaluates these files with the following setting:

`set script-extension off`

All scripts are always evaluated as [GDB] Command Files.

`set script-extension soft`

The debugger determines the scripting language based on filename extension. If this scripting language is supported, [GDB] Command File.

`set script-extension strict`

The debugger determines the scripting language based on filename extension, and evaluates the script using that language. If the language is not supported, then the evaluation fails.

`show script-extension`

Display the current value of the `script-extension` option.

---

• [Sequences](Sequences.html#Sequences) Commands
• [Aliases](Aliases.html#Aliases):                                                                       Command Aliases
• [Python](Python.html#Python) using Python
• [Guile](Guile.html#Guile) using Guile
• [Auto-loading extensions](Auto_002dloading-extensions.html#Auto_002dloading-extensions):               Automatically loading extensions
• [Multiple Extension Languages](Multiple-Extension-Languages.html#Multiple-Extension-Languages):        Working with multiple extension languages

---

---

::: header
Next: [Interpreters](Interpreters.html#Interpreters)]
:::
