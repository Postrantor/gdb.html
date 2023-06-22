---
description: Kill Process (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Kill Process (Debugging with GDB)
lang: en
resource-type: document
title: Kill Process (Debugging with GDB)
---
::: header
Next: [Inferiors Connections and Programs](Inferiors-Connections-and-Programs.html#Inferiors-Connections-and-Programs)]
:::

---

### 4.8 Killing the Child Process

`kill`

Kill the child process in which your program is running under [GDB].

This command is useful if you wish to debug a core dump instead of a running process. [GDB] ignores any core dump file while your program is running.

On some operating systems, a program cannot be executed outside [GDB]. You can use the `kill` command in this situation to permit running your program outside the debugger.

The `kill` command is also useful if you wish to recompile and relink your program, since on many systems it is impossible to modify an executable file while it is running in a process. In this case, when you next type `run`, [GDB] notices that the file has changed, and reads the symbol table again (while trying to preserve your current breakpoint settings).
