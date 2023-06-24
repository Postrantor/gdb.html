---
tip: translate by openai@2023-06-23 22:13:35
...
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

> 随着新的命令和功能定期添加到[GDB/MI]中关于目标支持某些特性。

#### The `-info-gdb-mi-command` Command

#### Synopsis

::: smallexample

```bash
 -info-gdb-mi-command cmd_name
```

:::

Query support for the [GDB/MI].


Note that the dash (`-`) starting all [GDB/MI]. However, for ease of use, this command also accepts the form with the leading dash.

> 注意，所有[GDB/MI]都以破折号（`-`）开头。但为了方便使用，此命令也接受带有前导破折号的形式。

#### [GDB]

There is no corresponding [GDB] command.

#### Result

The result is a tuple. There is currently only one field:

'`exists`'


:   This field is equal to `"true"` if the [GDB/MI] command exists, `"false"` otherwise.

> 这个字段等于"true"，如果[GDB/MI]命令存在，否则等于"false"。

#### Example

Here is an example where the [GDB/MI] command does not exist:

::: smallexample

```bash
-info-gdb-mi-command unsupported-command
^done,command=
```

:::


And here is an example where the [GDB/MI] command is known to the debugger:

> 这里有一个例子，调试器已经知道[GDB/MI]命令：

::: smallexample

```bash
-info-gdb-mi-command symbol-list-lines
^done,command=
```

:::

#### The `-list-features` Command


Returns a list of particular features of the MI protocol that this version of gdb implements. A feature can be a command, or a new field in an output of some command, or even an important bugfix. While a frontend can sometimes detect presence of a feature at runtime, it is easier to perform detection at debugger startup.

> 返回此版本的GDB实现的MI协议的特定功能列表。功能可以是命令，或某个命令输出中的新字段，甚至是重要的错误修复。虽然前端有时可以在运行时检测功能的存在，但在调试器启动时执行检测更容易。


The command returns a list of strings, with each string naming an available feature. Each returned string is just a name, it does not have any internal structure. The list of possible feature names is given below.

> 命令返回一个字符串列表，每个字符串命名一个可用的功能。每个返回的字符串只是一个名称，它没有任何内部结构。可能的特征名称列表如下。

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

> 表明支持`-var-set-frozen`命令，以及可能存在于`-varobj-create`输出中的`frozen`字段。

'`pending-breakpoints`

:   Indicates support for the `-f` option to the `-break-insert` command.

'`python`


:   Indicates Python scripting support, Python-based pretty-printing commands, and possible presence of the '`display_hint`' field in the output of `-var-list-children`

> ': 指示Python脚本支持，基于Python的精美打印命令，以及'-var-list-children'输出中可能存在的'display_hint'字段。

'`thread-info`

:   Indicates support for the `-thread-info` command.

'`data-read-memory-bytes`


:   Indicates support for the `-data-read-memory-bytes` and the `-data-write-memory-bytes` commands.

> 表明支持 `-data-read-memory-bytes` 和 `-data-write-memory-bytes` 命令。

'`breakpoint-notifications`


:   Indicates that changes to breakpoints and breakpoints created via the CLI will be announced via async records.

> 表示对断点以及通过CLI创建的断点的更改将通过异步记录进行公布。

'`ada-task-info`

:   Indicates support for the `-ada-task-info` command.

'`language-option`


:   Indicates that all [GDB/MI] option (see [Context management](Context-management.html#Context-management)).

> :表示所有[GDB/MI]选项（参见[上下文管理](Context-management.html#Context-management)）。

'`info-gdb-mi-command`

:   Indicates support for the `-info-gdb-mi-command` command.

'`undefined-command-error-code`


:   Indicates support for the \"undefined-command\" error code in error result records, produced when trying to execute an undefined [GDB/MI] command (see [GDB/MI Result Records](GDB_002fMI-Result-Records.html#GDB_002fMI-Result-Records)).

> 表示支持在试图执行未定义的[GDB/MI]命令时生成的错误结果记录中的“未定义命令”错误码（请参见[GDB/MI结果记录](GDB_002fMI-Result-Records.html#GDB_002fMI-Result-Records)）。

'`exec-run-start-option`


:   Indicates that the `-exec-run` command supports the `--start` option (see [GDB/MI Program Execution](GDB_002fMI-Program-Execution.html#GDB_002fMI-Program-Execution)).

> 指示`-exec-run`命令支持`--start`选项（参见[GDB/MI程序执行](GDB_002fMI-Program-Execution.html#GDB_002fMI-Program-Execution)）。

'`data-disassemble-a-option`


:   Indicates that the `-data-disassemble` command supports the `-a` option (see [GDB/MI Data Manipulation](GDB_002fMI-Data-Manipulation.html#GDB_002fMI-Data-Manipulation)).

> 指示`-data-disassemble`命令支持`-a`选项（请参阅[GDB/MI数据操作](GDB_002fMI-Data-Manipulation.html#GDB_002fMI-Data-Manipulation)）。

'`simple-values-ref-types`


:   Indicates that the `--simple-values` argument to the `-stack-list-arguments`, `-stack-list-locals`, `-stack-list-variables`, and `-var-list-children` commands takes reference types into account: that is, a value is considered simple if it is neither an array, structure, or union, nor a reference to an array, structure, or union.

> 指示`-stack-list-arguments`、`-stack-list-locals`、`-stack-list-variables`和`-var-list-children`命令的`--simple-values`参数考虑参考类型：也就是说，如果值既不是数组、结构体或联合，也不是对数组、结构体或联合的引用，则认为该值是简单的。

#### The `-list-target-features` Command


Returns a list of particular features that are supported by the target. Those features affect the permitted MI commands, but unlike the features reported by the `-list-features` command, the features depend on which target GDB is using at the moment. Whenever a target can change, due to commands such as `-target-select`, `-target-attach` or `-exec-run`, the list of target features may change, and the frontend should obtain it again. Example output:

> 返回一个受目标支持的特定功能列表。这些功能会影响允许的 MI 命令，但与 `-list-features` 命令报告的功能不同，这些功能取决于 GDB 当前使用的目标。每当目标可能因 `-target-select`、`-target-attach` 或 `-exec-run` 等命令而改变时，目标功能列表可能会改变，前端应该重新获取它。示例输出：

::: smallexample

```bash
(gdb) -list-target-features
^done,result=["async"]
```

:::

The current list of features is:

'`async`'


:   Indicates that the target is capable of asynchronous command execution, which means that [GDB] will accept further commands while the target is running.

> 表明目标能够进行异步命令执行，这意味着[GDB]在目标运行时可以接受更多的命令。

'`reverse`'


:   Indicates that the target is capable of reverse execution. See [Reverse Execution](Reverse-Execution.html#Reverse-Execution), for more information.

> 表明目标具有反向执行能力。有关更多信息，请参阅[反向执行](Reverse-Execution.html#Reverse-Execution)。

---

::: header
Next: [GDB/MI Miscellaneous Commands](GDB_002fMI-Miscellaneous-Commands.html#GDB_002fMI-Miscellaneous-Commands)]
:::
