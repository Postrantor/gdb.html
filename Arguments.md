---
description: Arguments (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Arguments (Debugging with GDB)
lang: en
resource-type: document
title: Arguments (Debugging with GDB)
---
::: header
Next: [Environment](Environment.html#Environment)]
:::

---

### 4.3 Your Program's Arguments

The arguments to your program can be specified by the arguments of the `run` command. They are passed to a shell, which expands wildcard characters and performs redirection of I/O, and thence to your program. Your `SHELL` environment variable (if it exists) specifies what shell [GDB] on Unix).

On non-Unix systems, the program is usually invoked directly by [GDB], which emulates I/O redirection via the appropriate system calls, and the wildcard characters are expanded by the startup code of the program, not by the shell.

`run` with no arguments uses the same arguments used by the previous `run`, or those set by the `set args` command.

`set args`

Specify the arguments to be used the next time your program is run. If `set args` has no arguments, `run` executes your program with no arguments. Once you have run your program with arguments, using `set args` before the next `run` is the only way to run it again without arguments.

`show args`

Show the arguments to give your program when it is started.
