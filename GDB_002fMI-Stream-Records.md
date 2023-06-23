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

`"~" string-output`

:   The console output stream contains text that should be displayed in the CLI console window. It contains the textual responses to CLI commands.

`"@" string-output`

:   The target output stream contains any textual output from the running target. This is only present when GDB's event loop is truly asynchronous, which is currently only the case for remote targets.

`"&" string-output`

:   The log stream contains debugging messages being produced by [GDB]'s internals.
