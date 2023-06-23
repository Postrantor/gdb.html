---
tip: translate by openai@2023-06-23 12:31:19
...
---
description: Running Configure (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Running Configure (Debugging with GDB)
lang: en
resource-type: document
title: Running Configure (Debugging with GDB)
---------------------------------------------

::: header
Next: [Separate Objdir](Separate-Objdir.html#Separate-Objdir)]
:::

---

### C.2 Invoking the [GDB]

[GDB] for installation; you can then use `make` to build the `gdb` program.

> 要安装[GDB]，您可以使用 `make` 来构建 `gdb` 程序。

The [GDB]'.

For example, the [GDB] directory. That directory contains:

> 例如，[GDB] 目录。该目录包含：

`gdb-14.0.50.20230622-git/configure (and supporting files)`

:   script for configuring [GDB] and all its supporting libraries

> 脚本用于配置 GDB 及其所有支持的库。

`gdb-14.0.50.20230622-git/gdb`

:   the source specific to [GDB] itself

> 这个特定于 GDB 本身。

`gdb-14.0.50.20230622-git/bfd`

:   source for the Binary File Descriptor library

> 源于二进制文件描述符库

`gdb-14.0.50.20230622-git/include`

:   [GNU] include files

`gdb-14.0.50.20230622-git/libiberty`

:   source for the '`-liberty`' free software library

> 自由软件库'`-liberty`'的源

`gdb-14.0.50.20230622-git/opcodes`

:   source for the library of opcode tables and disassemblers

> 虚拟机操作码表和反汇编器的资源库

`gdb-14.0.50.20230622-git/readline`

:   source for the [GNU] command-line interface

> 源代码用于[GNU]命令行界面

There may be other subdirectories as well.

> 可能还有其他的子目录。

The simplest way to configure and build [GDB] directory.

> 最简单的方法来配置和构建 GDB 目录。

First switch to the `gdb-version-number` will run as an argument.

> 首先将 `gdb-version-number` 切换到作为参数运行。

For example:

::: smallexample

```bash
cd gdb-14.0.50.20230622-git
./configure
make
```

:::

Running '`configure`' and then running `make` builds the included supporting libraries, then `gdb` itself. The configured source files, and the binaries, are left in the corresponding source directories.

> 运行 `configure` 然后运行 `make` 构建包含的支持库，然后是 `gdb` 本身。配置的源文件和二进制文件将留在相应的源目录中。

`configure` is a Bourne-shell (`/bin/sh`) script; if your system does not recognize this automatically when you run a different shell, you may need to run `sh` on it explicitly:

::: smallexample

```bash
sh configure
```

:::

You should run the `configure`.

> 你应该运行 `configure`。

You can install `GDB` anywhere. The best way to do this is to pass the `--prefix` option to `configure`, and then install it with `make install`.

> 你可以在任何地方安装 GDB。最好的方法是给 configure 传递--prefix 选项，然后用 make install 安装它。

---

::: header
Next: [Separate Objdir](Separate-Objdir.html#Separate-Objdir)]
:::
