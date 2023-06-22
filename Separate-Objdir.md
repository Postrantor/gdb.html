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

To build `gdb` in a separate directory, run `configure`' option; it is assumed.)

For example, with version 14.0.50.20230622-git, you can build [GDB] in a separate directory for a Sun 4 like this:

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

The `Makefile` that `configure`'), you will build all the required libraries, and then build GDB.

When you have multiple hosts or targets configured in separate directories, you can run `make` on them in parallel (for example, if they are NFS-mounted on each of the hosts); they will not interfere with each other.

---

::: header
Next: [Config Names](Config-Names.html#Config-Names)]
:::
