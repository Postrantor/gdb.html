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

The auto-loading feature is useful for supplying application-specific debugging commands and scripts.

Auto-loading can be enabled or disabled, and the list of auto-loaded scripts can be printed.

`set auto-load python-scripts [on|off]`

Enable or disable the auto-loading of Python scripts.

`show auto-load python-scripts`

Show whether auto-loading of Python scripts is enabled or disabled.

`info auto-load python-scripts [regexp]`

Print the list of all Python scripts that [GDB] auto-loaded.

Also printed is the list of Python scripts that were mentioned in the `.debug_gdb_scripts` section and were either not found (see [dotdebug_gdb_scripts section](dotdebug_005fgdb_005fscripts-section.html#dotdebug_005fgdb_005fscripts-section)) or were not auto-loaded due to `auto-load safe-path` rejection (see [Auto-loading](Auto_002dloading.html#Auto_002dloading)). This is useful because their names are not printed when [GDB] tries to load them and fails. There may be many of them, and printing an error message for each one is problematic.

If `regexp` is supplied only Python scripts with matching names are printed.

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

---

::: header
Next: [Python modules](Python-modules.html#Python-modules)]
:::
