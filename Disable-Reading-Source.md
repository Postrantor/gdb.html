---
tip: translate by openai@2023-06-23 20:32:10
...
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

> 在某些情况下，可能需要阻止GDB访问源代码文件。一种可能需要这样做的情况是，如果源代码文件位于网络连接速度较慢的网络中。


The following command can be used to control whether [GDB] should access source code files or not:

> 以下命令可用于控制[GDB]是否访问源代码文件：

`set source open [on|off]`

`show source open`


When this option is `on`, which is the default, [GDB] stops, or in response to the `list` command.

> 当这个选项处于默认状态“开”时，[GDB]会停止，或者响应“list”命令。

When this option is `off`, [GDB] will not access source code files.
