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

`--with-system-gdbinit-dir=directory`

:   Specify that the default location of the system-wide init file directory is `directory`.

If [GDB], they may be subject to relocation. Two possible cases:

- If the default location of this init file/directory contains `$prefix`.
- By contrast, if the default location does not contain the prefix, it will not be relocated. E.g. if [GDB] is installed.

If the configured location of the system-wide init file (as given by the `--with-system-gdbinit` has started with the `set data-directory` command, the file will not be reread.

This applies similarly to the system-wide directory specified in `--with-system-gdbinit-dir`.

Any supported scripting language can be used for these init files, as long as the file extension matches the scripting language. To be interpreted as regular [GDB] extension.

---

• [System-wide Configuration Scripts](System_002dwide-Configuration-Scripts.html#System_002dwide-Configuration-Scripts):        Installed System-wide Configuration Scripts

---

---

::: header
Previous: [Configure Options](Configure-Options.html#Configure-Options)]
:::
