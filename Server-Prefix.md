---
tip: translate by openai@2023-06-23 12:47:10
...
---
description: Server Prefix (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Server Prefix (Debugging with GDB)
lang: en
resource-type: document
title: Server Prefix (Debugging with GDB)
---
::: header
Next: [Prompting](Prompting.html#Prompting)]
:::

---

### 28.2 The Server Prefix


If you prefix a command with '`server `'s notion of which command to repeat if RET is pressed on a line by itself. This means that commands can be run behind a user's back by a front-end in a transparent manner.

> 如果你在一行的末尾按下RET，且在命令前加上'server'，则服务器会重复该命令。这意味着，前端可以以透明的方式在用户背后运行命令。


The `server ` prefix does not affect the recording of values into the value history; to print a value without recording it into the value history, use the `output` command instead of the `print` command.

> 服务器前缀不会影响值记录到值历史中；要打印一个值而不将其记录到值历史中，请使用`output`命令而不是`print`命令。


Using this prefix also disables confirmation requests (see [confirmation requests](Messages_002fWarnings.html#confirmation-requests)).

> 使用此前缀也会禁用确认请求（参见[确认请求](Messages_002fWarnings.html#confirmation-requests)）。
