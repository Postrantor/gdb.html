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

The auto-loading feature is useful for supplying application-specific debugging commands and scripts.

Auto-loading can be enabled or disabled, and the list of auto-loaded scripts can be printed.

`set auto-load guile-scripts [on|off]`

Enable or disable the auto-loading of Guile scripts.

`show auto-load guile-scripts`

Show whether auto-loading of Guile scripts is enabled or disabled.

`info auto-load guile-scripts [regexp]`

Print the list of all Guile scripts that [GDB] auto-loaded.

Also printed is the list of Guile scripts that were mentioned in the `.debug_gdb_scripts` section and were not found. This is useful because their names are not printed when [GDB] tries to load them and fails. There may be many of them, and printing an error message for each one is problematic.

If `regexp` is supplied only Guile scripts with matching names are printed.

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
