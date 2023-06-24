---
tip: translate by openai@2023-06-23 22:13:07
...
---
description: GDB/MI Stream Records (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: GDB/MI Stream Records (Debugging with GDB)
lang: en
resource-type: document
title: GDB/MI Stream Records (Debugging with GDB)
---
::: header
Next: [GDB/MI Async Records](GDB_002fMI-Async-Records.html#GDB_002fMI-Async-Records)]
:::

---

#### 27.5.2 [GDB/MI]

[GDB] interface using *stream records*.


Each stream record begins with a unique *prefix character* which identifies its stream (see [[GDB/MI] Output Syntax](GDB_002fMI-Output-Syntax.html#GDB_002fMI-Output-Syntax)). In addition to the prefix, each stream record contains a `string-output`. This is either raw text (with an implicit new line) or a quoted C string (which does not contain an implicit newline).

> 每条流记录都以一个唯一的*前缀字符*开头，用于标识其流（参见[[GDB/MI] Output Syntax](GDB_002fMI-Output-Syntax.html#GDB_002fMI-Output-Syntax)）。除了前缀之外，每条流记录还包含一个`string-output`。这可以是原始文本（带有隐式新行），也可以是引用的C字符串（不包含隐式换行符）。

`"~" string-output`


:   The console output stream contains text that should be displayed in the CLI console window. It contains the textual responses to CLI commands.

> 控制台输出流包含应在CLI控制台窗口中显示的文本。它包含CLI命令的文本响应。

`"@" string-output`


:   The target output stream contains any textual output from the running target. This is only present when GDB's event loop is truly asynchronous, which is currently only the case for remote targets.

> 目标输出流包含运行目标的任何文本输出。这只有在GDB的事件循环真正异步的情况下才会出现，目前仅对远程目标有效。

`"&" string-output`


:   The log stream contains debugging messages being produced by [GDB]'s internals.

> 日志流包含GDB内部产生的调试消息。
