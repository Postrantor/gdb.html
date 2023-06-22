---
description: Data Files (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Data Files (Debugging with GDB)
lang: en
resource-type: document
title: Data Files (Debugging with GDB)
---
::: header
Previous: [Symbol Errors](Symbol-Errors.html#Symbol-Errors)]
:::

---

### 18.7 GDB Data Files

[GDB] will sometimes read an auxiliary data file. These files are kept in a directory known as the *data directory*.

You can set the data directory's name, and view the name [GDB] is currently using.

`set data-directory directory`

Set the directory which [GDB].

`show data-directory`

Show the directory [GDB] searches for auxiliary data files.

You can set the default data directory by using the configure-time '`--with-gdb-datadir` is moved to a new location.

The data directory may also be specified with the `--data-directory` command line option. See [Mode Options](Mode-Options.html#Mode-Options).
