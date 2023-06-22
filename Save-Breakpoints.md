---
description: Save Breakpoints (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Save Breakpoints (Debugging with GDB)
lang: en
resource-type: document
title: Save Breakpoints (Debugging with GDB)
---
::: header
Next: [Static Probe Points](Static-Probe-Points.html#Static-Probe-Points)]
:::

---

#### 5.1.9 How to save breakpoints to a file

To save breakpoint definitions to a file use the `save breakpoints` command.

`save breakpoints [filename]`

This command saves all current breakpoint definitions together with their commands and ignore counts, into a file `filename` commands that recreate the breakpoints, you can edit the file in your favorite editing program, and remove the breakpoint definitions you're not interested in, or that can no longer be recreated.
