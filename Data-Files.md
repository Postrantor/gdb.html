---
tip: translate by openai@2023-06-23 20:12:41
...
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

> [GDB] 有时会读取辅助数据文件。这些文件存放在一个被称为*数据目录*的目录中。


You can set the data directory's name, and view the name [GDB] is currently using.

> 你可以设置数据目录的名称，并查看[GDB]当前正在使用的名称。

`set data-directory directory`

Set the directory which [GDB].

`show data-directory`

Show the directory [GDB] searches for auxiliary data files.


You can set the default data directory by using the configure-time '`--with-gdb-datadir` is moved to a new location.

> 你可以通过使用配置时的'--with-gdb-datadir'将默认数据目录移动到新位置。


The data directory may also be specified with the `--data-directory` command line option. See [Mode Options](Mode-Options.html#Mode-Options).

> 数据目录也可以使用 `--data-directory` 命令行选项指定。参见 [模式选项](Mode-Options.html#Mode-Options)。
