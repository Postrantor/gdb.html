---
description: Invoking GDB (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Invoking GDB (Debugging with GDB)
lang: en
resource-type: document
title: Invoking GDB (Debugging with GDB)
---
::: header
Next: [Quitting GDB](Quitting-GDB.html#Quitting-GDB)]
:::

---

### 2.1 Invoking [GDB]

Invoke [GDB] reads commands from the terminal until you tell it to exit.

You can also run `gdb` with a variety of arguments and options, to specify more of your debugging environment at the outset.

The command-line options described here are designed to cover a variety of situations; in some environments, some of these options may effectively be unavailable.

The most usual way to start [GDB] is with one argument, specifying an executable program:

::: smallexample

```bash
gdb program
```

:::

You can also start with both an executable program and a core file specified:

::: smallexample

```bash
gdb program core
```

:::

You can, instead, specify a process ID as a second argument or use option `-p`, if you want to debug a running process:

::: smallexample

```bash
gdb program 1234
gdb -p 1234
```

:::

would attach [GDB] filename.

Taking advantage of the second command-line argument requires a fairly complete operating system; when you use [GDB] will warn you if it is unable to attach or to read core dumps.

You can optionally have `gdb` pass any arguments after the executable file to the inferior using `--args`. This option stops option processing.

::: smallexample

```bash
gdb --args gcc -O2 -c foo.c
```

:::

This will cause `gdb` to debug `gcc`, and to set `gcc`'s command-line arguments (see [Arguments](Arguments.html#Arguments)) to '`-O2 -c foo.c`'.

You can run `gdb` without printing the front material, which describes [GDB]'s non-warranty, by specifying `--silent` (or `-q`/`--quiet`):

::: smallexample

```bash
gdb --silent
```

:::

You can further control how [GDB] itself can remind you of the options available.

Type

::: smallexample

```bash
gdb -help
```

:::

to display all available options and briefly describe their use ('`gdb -h`' is a shorter equivalent).

All options and command line arguments you give are processed in sequential order. The order makes a difference when the '`-x`' option is used.

---

• [File Options](File-Options.html#File-Options):                                Choosing files
• [Mode Options](Mode-Options.html#Mode-Options):                                Choosing modes
• [Startup](Startup.html#Startup) does during startup
• [Initialization Files](Initialization-Files.html#Initialization-Files):        Initialization Files

---

---

::: header
Next: [Quitting GDB](Quitting-GDB.html#Quitting-GDB)]
:::
