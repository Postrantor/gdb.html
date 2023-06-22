---
description: Working Directory (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Working Directory (Debugging with GDB)
lang: en
resource-type: document
title: Working Directory (Debugging with GDB)
---
::: header
Next: [Input/Output](Input_002fOutput.html#Input_002fOutput)]
:::

---

### 4.5 Your Program's Working Directory

Each time you start your program with `run`, the inferior will be initialized with the current working directory specified by the [set cwd]'s current working directory as its working directory if native debugging, or it will inherit the remote server's current working directory if remote debugging.

`set cwd [directory]`

Set the inferior's working directory to `directory` uses the concatenation of `HOMEDRIVE` and `HOMEPATH` as fallback.

You can also change [GDB]'s current working directory by using the `cd` command. See [cd command](#cd-command).

`show cwd`

Show the inferior's working directory. If no directory has been specified by [set cwd]'s working directory.

`cd [directory]`

Set the [GDB].

The [GDB] to operate on. See [Commands to Specify Files](Files.html#Files). See [set cwd command](#set-cwd-command).

`pwd`

Print the [GDB] working directory.

It is generally impossible to find the current working directory of the process being debugged (since a program can change its directory during its run). If you work on a system where [GDB] supports the `info proc` command (see [Process Information](Process-Information.html#Process-Information)), you can use the `info proc` command to find out the current working directory of the debuggee.

---

::: header
Next: [Input/Output](Input_002fOutput.html#Input_002fOutput)]
:::
