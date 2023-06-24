---
tip: translate by openai@2023-06-24 02:28:55
...
---
description: Separate Objdir (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Separate Objdir (Debugging with GDB)
lang: en
resource-type: document
title: Separate Objdir (Debugging with GDB)
---
::: header
Next: [Config Names](Config-Names.html#Config-Names)]
:::

---

### C.3 Compiling [GDB]


If you want to run [GDB] `make` does), running `make` in each of these directories builds the `gdb` program specified there.

> 如果你想运行[GDB]，在每个目录中运行`make`就可以构建那里指定的`gdb`程序。


To build `gdb` in a separate directory, run `configure`' option; it is assumed.)

> 在一个单独的目录中构建`gdb`，运行`configure`选项；这是假定的。


For example, with version 14.0.50.20230622-git, you can build [GDB] in a separate directory for a Sun 4 like this:

> 例如，使用版本14.0.50.20230622-git，您可以像这样在一个单独的目录中为Sun 4构建[GDB]：

::: smallexample

```bash
cd gdb-14.0.50.20230622-git
mkdir ../gdb-sun4
cd ../gdb-sun4
../gdb-14.0.50.20230622-git/configure
make
```

:::

When `configure`.

Make sure that your path to the `configure`.

One popular reason to build several [GDB].


When you run `make` to build a program or library, you must run it in a configured directory---whatever directory you were in when you called `configure` (or one of its subdirectories).

> 当你运行`make`来构建一个程序或库时，你必须在一个配置的目录里运行它---无论你在调用`configure`时在哪个目录下。


The `Makefile` that `configure`'), you will build all the required libraries, and then build GDB.

> `configure` 所需的 `Makefile`，将构建所有必要的库，然后构建 GDB。


When you have multiple hosts or targets configured in separate directories, you can run `make` on them in parallel (for example, if they are NFS-mounted on each of the hosts); they will not interfere with each other.

> 当你在不同的目录中配置了多个主机或目标时，你可以并行运行 `make`（例如，如果它们在每个主机上都是NFS 挂载的），它们不会相互干扰。

---

::: header
Next: [Config Names](Config-Names.html#Config-Names)]
:::
