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

This feature may be removed at some stage in the future and it is recommended that front ends use the `-interpreter-exec` command (see [-interpreter-exec](GDB_002fMI-Miscellaneous-Commands.html#g_t_002dinterpreter_002dexec)).
