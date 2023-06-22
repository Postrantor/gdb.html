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

Auto-loading can be enabled or disabled, and the list of auto-loaded scripts can be printed.

`set auto-load gdb-scripts [on|off]`

Enable or disable the auto-loading of canned sequences of commands scripts.

`show auto-load gdb-scripts`

Show whether auto-loading of canned sequences of commands scripts is enabled or disabled.

`info auto-load gdb-scripts [regexp]`

Print the list of all canned sequences of commands scripts that [GDB] auto-loaded.

If `regexp` is supplied only canned sequences of commands scripts with matching names are printed.
