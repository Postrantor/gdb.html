---
description: GDB/MI Output Syntax (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: GDB/MI Output Syntax (Debugging with GDB)
lang: en
resource-type: document
title: GDB/MI Output Syntax (Debugging with GDB)
---
::: header
Previous: [GDB/MI Input Syntax](GDB_002fMI-Input-Syntax.html#GDB_002fMI-Input-Syntax)]
:::

---

#### 27.2.2 [GDB/MI]

The output from [GDB/MI]'.

If an input command was prefixed with a `token` then the corresponding output for that command will also be prefixed by that same `token`.

`output →`

:   `( out-of-band-record )* [ result-record ] "(gdb)" nl`

`result-record →`

:   ` [ token ] "^" result-class ( "," result )* nl`

`out-of-band-record →`

:   `async-record | stream-record`

`async-record →`

:   `exec-async-output | status-async-output | notify-async-output`

`exec-async-output →`

:   `[ token ] "*" async-output nl`

`status-async-output →`

:   `[ token ] "+" async-output nl`

`notify-async-output →`

:   `[ token ] "=" async-output nl`

`async-output →`

:   `async-class ( "," result )*`

`result-class →`

:   `"done" | "running" | "connected" | "error" | "exit"`

`async-class →`

:   `"stopped" | others` (where `others` will be added depending on the needs---this is still in development).

`result →`

:   ` variable "=" value`

`variable →`

:   `string`

`value →`

:   `const | tuple | list`

`const →`

:   `c-string`

`tuple →`

:   `""`

`list →`

:   `"" | "[" value ( "," value )* "]" | "[" result ( "," result )* "]"`

`stream-record →`

:   `console-stream-output | target-stream-output | log-stream-output`

`console-stream-output →`

:   `"~" c-string nl`

`target-stream-output →`

:   `"@" c-string nl`

`log-stream-output →`

:   `"&" c-string nl`

`nl →`

:   `CR | CR-LF`

`token →`

:   *any sequence of digits*.

Notes:

- All output sequences end in a single line containing a period.
- The `token` is from the corresponding request. Note that for all async output, while the token is allowed by the grammar and may be output by future versions of [GDB] for select async output messages, it is generally omitted. Frontends should treat all async output as reporting general changes in the state of the target and there should be no need to associate async output to any prior command.
- '.
- '.
- '.
- '.
- '.
- '.
- .

See [[GDB/MI] Stream Records](GDB_002fMI-Stream-Records.html#GDB_002fMI-Stream-Records), for more details about the various output records.

---

::: header
Previous: [GDB/MI Input Syntax](GDB_002fMI-Input-Syntax.html#GDB_002fMI-Input-Syntax)]
:::
