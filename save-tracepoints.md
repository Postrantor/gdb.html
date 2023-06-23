---
tip: translate by openai@2023-06-23 12:35:38
...
---
description: save tracepoints (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: save tracepoints (Debugging with GDB)
lang: en
resource-type: document
title: save tracepoints (Debugging with GDB)
--------------------------------------------

::: header
Previous: [tdump](tdump.html#tdump)]
:::

---

#### 13.2.3 `save tracepoints filename`

This command saves all current tracepoint definitions together with their actions and passcounts, into a file `filename` suitable for use in a later debugging session. To read the saved tracepoint definitions, use the `source` command (see [Command Files](Command-Files.html#Command-Files)). The `save-tracepoints` command is a deprecated alias for `save tracepoints`

> 这个命令将所有当前跟踪点定义以及它们的操作和 passcounts 保存到一个名为 `filename` 的文件中，以便在以后的调试会话中使用。要读取保存的跟踪点定义，请使用 `source` 命令（参见[命令文件](Command-Files.html#Command-Files)）。`save-tracepoints` 命令是 `save tracepoints` 的废弃别名。
