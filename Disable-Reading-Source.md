---
description: Disable Reading Source (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Disable Reading Source (Debugging with GDB)
lang: en
resource-type: document
title: Disable Reading Source (Debugging with GDB)
---
::: header
Previous: [Machine Code](Machine-Code.html#Machine-Code)]
:::

---

### 9.7 Disable Reading Source Code

In some cases it can be desirable to prevent [GDB] from accessing source code files. One case where this might be desirable is if the source code files are located over a slow network connection.

The following command can be used to control whether [GDB] should access source code files or not:

`set source open [on|off]`

`show source open`

When this option is `on`, which is the default, [GDB] stops, or in response to the `list` command.

When this option is `off`, [GDB] will not access source code files.
