---
description: GDB/MI Ada Exceptions Commands (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: GDB/MI Ada Exceptions Commands (Debugging with GDB)
lang: en
resource-type: document
title: GDB/MI Ada Exceptions Commands (Debugging with GDB)
---
::: header
Next: [GDB/MI Support Commands](GDB_002fMI-Support-Commands.html#GDB_002fMI-Support-Commands)]
:::

---

### 27.22 Ada Exceptions [GDB/MI]

#### The `-info-ada-exceptions` Command

#### Synopsis

::: smallexample

```bash
 -info-ada-exceptions [ regexp]
```

:::

List all Ada exceptions defined within the program being debugged. With a regular expression `regexp` are listed.

#### [GDB]

The corresponding [GDB]'.

#### Result

The result is a table of Ada exceptions. The following columns are defined for each exception:

'`name`'

:   The name of the exception.

'`address`'

:   The address of the exception.

#### Example

::: smallexample

```bash
-info-ada-exceptions aint
^done,ada-exceptions={nr_rows="2",nr_cols="2",
hdr=[,
],
body=[,

```

:::

#### Catching Ada Exceptions

The commands describing how to ask [GDB] to stop when a program raises an exception are described at [Ada Exception GDB/MI Catchpoint Commands](Ada-Exception-GDB_002fMI-Catchpoint-Commands.html#Ada-Exception-GDB_002fMI-Catchpoint-Commands).
