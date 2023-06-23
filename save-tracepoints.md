---
description: save tracepoints (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: save tracepoints (Debugging with GDB)
lang: en
resource-type: document
title: save tracepoints (Debugging with GDB)
---
::: header
Previous: [tdump](tdump.html#tdump)]
:::

---

#### 13.2.3 `save tracepoints filename`

This command saves all current tracepoint definitions together with their actions and passcounts, into a file `filename` suitable for use in a later debugging session. To read the saved tracepoint definitions, use the `source` command (see [Command Files](Command-Files.html#Command-Files)). The `save-tracepoints` command is a deprecated alias for `save tracepoints`
