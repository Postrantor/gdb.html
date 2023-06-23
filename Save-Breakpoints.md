---
tip: translate by openai@2023-06-23 12:35:26
...
---
description: Save Breakpoints (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Save Breakpoints (Debugging with GDB)
lang: en
resource-type: document
title: Save Breakpoints (Debugging with GDB)
--------------------------------------------

::: header
Next: [Static Probe Points](Static-Probe-Points.html#Static-Probe-Points)]
:::

---

#### 5.1.9 How to save breakpoints to a file

To save breakpoint definitions to a file use the `save breakpoints` command.

> 使用 `save breakpoints` 命令将断点定义保存到文件中。

`save breakpoints [filename]`

This command saves all current breakpoint definitions together with their commands and ignore counts, into a file `filename` commands that recreate the breakpoints, you can edit the file in your favorite editing program, and remove the breakpoint definitions you're not interested in, or that can no longer be recreated.

> 这个命令将所有当前断点定义以及它们的命令和忽略计数保存到文件 `filename` 中，这些命令可以重新创建断点，您可以在您喜欢的编辑程序中编辑该文件，并删除您不感兴趣的断点定义或无法重新创建的断点定义。
