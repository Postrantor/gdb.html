---
description: GDB/MI Input Syntax (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: GDB/MI Input Syntax (Debugging with GDB)
lang: en
resource-type: document
title: GDB/MI Input Syntax (Debugging with GDB)
---
::: header
Next: [GDB/MI Output Syntax](GDB_002fMI-Output-Syntax.html#GDB_002fMI-Output-Syntax)]
:::

---

#### 27.2.1 [GDB/MI]

`command →`

:   `cli-command | mi-command`

`cli-command →`

:   `[ token ] cli-command nl`, where `cli-command` CLI command.

`mi-command →`

:   `[ token ] "-" operation ( " " option )* [` \" \--\" `]` ( \" \" `parameter`

`token →`

:   \"any sequence of digits\"

`option →`

:   `"-" parameter [ " " parameter ]`

`parameter →`

:   `non-blank-sequence | c-string`

`operation →`

:   *any of the operations described in this chapter*

`non-blank-sequence →`

:   *anything, provided it doesn't contain special characters such as \"-\", `nl`, \"\"\" and of course \" \"*

`c-string →`

:   `""" seven-bit-iso-c-string-content """`

`nl →`

:   `CR | CR-LF`

Notes:

- The CLI commands are still handled by the [MI] interpreter; their output is described below.
- The `token`, when present, is passed back when the command finishes.
- Some [MI]' (this is useful when some parameters begin with a dash).

Pragmatics:

- We want easy access to the existing CLI syntax (for debugging).
- We want it to be easy to spot a [MI] operation.
