---
description: GDB/MI Support Commands (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: GDB/MI Support Commands (Debugging with GDB)
lang: en
resource-type: document
title: GDB/MI Support Commands (Debugging with GDB)
---
::: header
Next: [GDB/MI Miscellaneous Commands](GDB_002fMI-Miscellaneous-Commands.html#GDB_002fMI-Miscellaneous-Commands)]
:::

---

### 27.23 [GDB/MI]

Since new commands and features get regularly added to [GDB/MI] about target support of certain features.

#### The `-info-gdb-mi-command` Command

#### Synopsis

::: smallexample

```bash
 -info-gdb-mi-command cmd_name
```

:::

Query support for the [GDB/MI].

Note that the dash (`-`) starting all [GDB/MI]. However, for ease of use, this command also accepts the form with the leading dash.

#### [GDB]

There is no corresponding [GDB] command.

#### Result

The result is a tuple. There is currently only one field:

'`exists`'

:   This field is equal to `"true"` if the [GDB/MI] command exists, `"false"` otherwise.

#### Example

Here is an example where the [GDB/MI] command does not exist:

::: smallexample

```bash
-info-gdb-mi-command unsupported-command
^done,command=
```

:::

And here is an example where the [GDB/MI] command is known to the debugger:

::: smallexample

```bash
-info-gdb-mi-command symbol-list-lines
^done,command=
```

:::

#### The `-list-features` Command

Returns a list of particular features of the MI protocol that this version of gdb implements. A feature can be a command, or a new field in an output of some command, or even an important bugfix. While a frontend can sometimes detect presence of a feature at runtime, it is easier to perform detection at debugger startup.

The command returns a list of strings, with each string naming an available feature. Each returned string is just a name, it does not have any internal structure. The list of possible feature names is given below.

Example output:

::: smallexample

```bash
(gdb) -list-features
^done,result=["feature1","feature2"]
```

:::

The current list of features is:

'`frozen-varobjs`

:   Indicates support for the `-var-set-frozen` command, as well as possible presence of the `frozen` field in the output of `-varobj-create`.

'`pending-breakpoints`

:   Indicates support for the `-f` option to the `-break-insert` command.

'`python`

:   Indicates Python scripting support, Python-based pretty-printing commands, and possible presence of the '`display_hint`' field in the output of `-var-list-children`

'`thread-info`

:   Indicates support for the `-thread-info` command.

'`data-read-memory-bytes`

:   Indicates support for the `-data-read-memory-bytes` and the `-data-write-memory-bytes` commands.

'`breakpoint-notifications`

:   Indicates that changes to breakpoints and breakpoints created via the CLI will be announced via async records.

'`ada-task-info`

:   Indicates support for the `-ada-task-info` command.

'`language-option`

:   Indicates that all [GDB/MI] option (see [Context management](Context-management.html#Context-management)).

'`info-gdb-mi-command`

:   Indicates support for the `-info-gdb-mi-command` command.

'`undefined-command-error-code`

:   Indicates support for the \"undefined-command\" error code in error result records, produced when trying to execute an undefined [GDB/MI] command (see [GDB/MI Result Records](GDB_002fMI-Result-Records.html#GDB_002fMI-Result-Records)).

'`exec-run-start-option`

:   Indicates that the `-exec-run` command supports the `--start` option (see [GDB/MI Program Execution](GDB_002fMI-Program-Execution.html#GDB_002fMI-Program-Execution)).

'`data-disassemble-a-option`

:   Indicates that the `-data-disassemble` command supports the `-a` option (see [GDB/MI Data Manipulation](GDB_002fMI-Data-Manipulation.html#GDB_002fMI-Data-Manipulation)).

'`simple-values-ref-types`

:   Indicates that the `--simple-values` argument to the `-stack-list-arguments`, `-stack-list-locals`, `-stack-list-variables`, and `-var-list-children` commands takes reference types into account: that is, a value is considered simple if it is neither an array, structure, or union, nor a reference to an array, structure, or union.

#### The `-list-target-features` Command

Returns a list of particular features that are supported by the target. Those features affect the permitted MI commands, but unlike the features reported by the `-list-features` command, the features depend on which target GDB is using at the moment. Whenever a target can change, due to commands such as `-target-select`, `-target-attach` or `-exec-run`, the list of target features may change, and the frontend should obtain it again. Example output:

::: smallexample

```bash
(gdb) -list-target-features
^done,result=["async"]
```

:::

The current list of features is:

'`async`'

:   Indicates that the target is capable of asynchronous command execution, which means that [GDB] will accept further commands while the target is running.

'`reverse`'

:   Indicates that the target is capable of reverse execution. See [Reverse Execution](Reverse-Execution.html#Reverse-Execution), for more information.

---

::: header
Next: [GDB/MI Miscellaneous Commands](GDB_002fMI-Miscellaneous-Commands.html#GDB_002fMI-Miscellaneous-Commands)]
:::
