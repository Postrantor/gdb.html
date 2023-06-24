---
tip: translate by openai@2023-06-24 04:47:20
...
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

> 每次您使用`run`启动程序，如果是本地调试，则被动程序将使用[set cwd]当前工作目录作为其工作目录初始化；如果是远程调试，则将继承远程服务器的当前工作目录。

`set cwd [directory]`


Set the inferior's working directory to `directory` uses the concatenation of `HOMEDRIVE` and `HOMEPATH` as fallback.

> 将下级工作目录设置为“目录”，如果失败，则使用“HOMEDRIVE”和“HOMEPATH”的连接。


You can also change [GDB]'s current working directory by using the `cd` command. See [cd command](#cd-command).

> 你也可以通过使用`cd`命令来改变GDB的当前工作目录。参见[cd命令](#cd-command)。

`show cwd`


Show the inferior's working directory. If no directory has been specified by [set cwd]'s working directory.

> 显示下级工作目录。如果没有由[设置cwd]指定的工作目录，则不指定。

`cd [directory]`

Set the [GDB].


The [GDB] to operate on. See [Commands to Specify Files](Files.html#Files). See [set cwd command](#set-cwd-command).

> GDB运行操作。参见[指定文件的命令](Files.html#Files)。参见[设置当前工作目录命令](#set-cwd-command)。

`pwd`

Print the [GDB] working directory.


It is generally impossible to find the current working directory of the process being debugged (since a program can change its directory during its run). If you work on a system where [GDB] supports the `info proc` command (see [Process Information](Process-Information.html#Process-Information)), you can use the `info proc` command to find out the current working directory of the debuggee.

> 一般来说，很难找到正在调试的进程的当前工作目录（因为程序在运行时可以更改其目录）。如果您在支持`info proc`命令的系统上工作（参见[进程信息](Process-Information.html#Process-Information)），可以使用`info proc`命令找出调试对象的当前工作目录。

---

::: header
Next: [Input/Output](Input_002fOutput.html#Input_002fOutput)]
:::
