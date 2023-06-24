---
tip: translate by openai@2023-06-23 23:46:17
...
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

> 如果您想要调试一个核心转储而不是一个正在运行的进程，这个命令很有用。[GDB] 在程序运行时会忽略任何核心转储文件。


On some operating systems, a program cannot be executed outside [GDB]. You can use the `kill` command in this situation to permit running your program outside the debugger.

> 在某些操作系统中，程序无法在GDB之外执行。您可以使用`kill`命令来允许在调试器外运行程序。


The `kill` command is also useful if you wish to recompile and relink your program, since on many systems it is impossible to modify an executable file while it is running in a process. In this case, when you next type `run`, [GDB] notices that the file has changed, and reads the symbol table again (while trying to preserve your current breakpoint settings).

> `kill` 命令如果你希望重新编译和重新链接你的程序也是很有用的，因为在许多系统中，当一个可执行文件正在进程中运行时是不可能修改它的。在这种情况下，当你下一次输入`run`时，[GDB] 会注意到文件已经改变，并重新读取符号表（同时尝试保持当前的断点设置）。
