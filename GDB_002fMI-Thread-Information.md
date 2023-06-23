---
description: GDB/MI Thread Information (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: GDB/MI Thread Information (Debugging with GDB)
lang: en
resource-type: document
title: GDB/MI Thread Information (Debugging with GDB)
---
::: header
Next: [GDB/MI Ada Exception Information](GDB_002fMI-Ada-Exception-Information.html#GDB_002fMI-Ada-Exception-Information)]
:::

---

#### 27.5.6 [GDB/MI]

Whenever [GDB] has to report an information about a thread, it uses a tuple with the following fields. The fields are always present unless stated otherwise.

`id`

:   The global numeric id assigned to the thread by [GDB].

`target-id`

:   The target-specific string identifying the thread.

`details`

:   Additional information about the thread provided by the target. It is supposed to be human-readable and not interpreted by the frontend. This field is optional.

`name`

:   The name of the thread. If the user specified a name using the `thread name` command, then this name is given. Otherwise, if [GDB] cannot find the thread name, then this field is omitted.

`state`

:   The execution state of the thread, either '`stopped`', depending on whether the thread is presently running.

`frame`

:   The stack frame currently executing in the thread. This field is only present if the thread is stopped. Its format is documented in [GDB/MI Frame Information](GDB_002fMI-Frame-Information.html#GDB_002fMI-Frame-Information).

`core`

:   The value of this field is an integer number of the processor core the thread was last seen on. This field is optional.
