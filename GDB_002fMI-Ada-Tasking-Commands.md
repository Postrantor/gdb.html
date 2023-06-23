---
description: GDB/MI Ada Tasking Commands (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: GDB/MI Ada Tasking Commands (Debugging with GDB)
lang: en
resource-type: document
title: GDB/MI Ada Tasking Commands (Debugging with GDB)
---
::: header
Next: [GDB/MI Program Execution](GDB_002fMI-Program-Execution.html#GDB_002fMI-Program-Execution)]
:::

---

### 27.12 [GDB/MI]

#### The `-ada-task-info` Command

#### Synopsis

::: smallexample

```bash
 -ada-task-info [ task-id ]
```

:::

Reports information about either a specific Ada task, if the `task-id` parameter is present, or about all Ada tasks.

#### [GDB]

The '`info tasks`' command prints the same information about all Ada tasks (see [Ada Tasks](Ada-Tasks.html#Ada-Tasks)).

#### Result

The result is a table of Ada tasks. The following columns are defined for each Ada task:

'`current`'

:   This field exists only for the current thread. It has the value '`*`'.

'`id`'

:   The identifier that [GDB] uses to refer to the Ada task.

'`task-id`'

:   The identifier that the target uses to refer to the Ada task.

'`thread-id`'

:   The global thread identifier of the thread corresponding to the Ada task.

```
This field should always exist, as Ada tasks are always implemented on top of a thread. But if [GDB] cannot find this corresponding thread for any reason, the field is omitted.
```

'`parent-id`'

:   This field exists only when the task was created by another task. In this case, it provides the ID of the parent task.

'`priority`'

:   The base priority of the task.

'`state`'

:   The current state of the task. For a detailed description of the possible states, see [Ada Tasks](Ada-Tasks.html#Ada-Tasks).

'`name`'

:   The name of the task.

#### Example

::: smallexample

```bash
-ada-task-info
^done,tasks={nr_rows="3",nr_cols="8",
hdr=[,
,
,
,
,
,
,
],
body=[{current="*",id="1",task-id="   644010",thread-id="1",priority="48",
state="Child Termination Wait",name="main_task"}]}
(gdb)
```

:::

---

::: header
Next: [GDB/MI Program Execution](GDB_002fMI-Program-Execution.html#GDB_002fMI-Program-Execution)]
:::
