---
description: GDB/MI Result Records (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: GDB/MI Result Records (Debugging with GDB)
lang: en
resource-type: document
title: GDB/MI Result Records (Debugging with GDB)
---
::: header
Next: [GDB/MI Stream Records](GDB_002fMI-Stream-Records.html#GDB_002fMI-Stream-Records)]
:::

---

#### 27.5.1 [GDB/MI]

In addition to a number of out-of-band notifications, the response to a [GDB/MI] command includes one of the following result indications:

`"^done" [ "," results ]`

The synchronous operation was successful, `results` are the return values.

`"^running"`

This result record is equivalent to '`^done`' output record to determine which threads are resumed.

`"^connected"`

[GDB] has connected to a remote target.

`"^error" "," "msg=" c-string [ "," "code=" c-string ]`

The operation failed. The `msg=c-string` variable contains the corresponding error message.

If present, the `code=c-string` variable provides an error code on which consumers can rely on to detect the corresponding error condition. At present, only one error code is defined:

'`"undefined-command"`'

:   Indicates that the command causing the error does not exist.

`"^exit"`

[GDB] has terminated.
