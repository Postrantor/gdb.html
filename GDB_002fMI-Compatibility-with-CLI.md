---
tip: translate by openai@2023-06-23 21:53:08
...
---
description: GDB/MI Compatibility with CLI (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: GDB/MI Compatibility with CLI (Debugging with GDB)
lang: en
resource-type: document
title: GDB/MI Compatibility with CLI (Debugging with GDB)
---
::: header
Next: [GDB/MI Development and Front Ends](GDB_002fMI-Development-and-Front-Ends.html#GDB_002fMI-Development-and-Front-Ends)]
:::

---

### 27.3 [GDB/MI]


For the developers convenience CLI commands can be entered directly, but there may be some unexpected behaviour. For example, commands that query the user will behave as if the user replied yes, breakpoint command lists are not executed and some CLI commands, such as `if`, `when` and `define`, prompt for further input with '`>`', which is not valid MI output.

> 为了方便开发者，可以直接输入CLI命令，但可能会有一些意外的行为。例如，查询用户的命令会表现得好像用户回答了"是"，断点命令列表不会被执行，而一些CLI命令，如`if`、`when`和`define`，会用'`>`'提示进一步输入，这在MI输出中是无效的。


This feature may be removed at some stage in the future and it is recommended that front ends use the `-interpreter-exec` command (see [-interpreter-exec](GDB_002fMI-Miscellaneous-Commands.html#g_t_002dinterpreter_002dexec)).

> 这个功能可能会在将来的某个阶段被移除，因此建议前端使用`-interpreter-exec`命令（参见[-interpreter-exec](GDB_002fMI-Miscellaneous-Commands.html#g_t_002dinterpreter_002dexec)）。
