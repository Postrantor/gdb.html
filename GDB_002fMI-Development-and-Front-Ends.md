---
tip: translate by openai@2023-06-24 10:17:06
...
---
description: GDB/MI Development and Front Ends (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: GDB/MI Development and Front Ends (Debugging with GDB)
lang: en
resource-type: document
title: GDB/MI Development and Front Ends (Debugging with GDB)
---
::: header
Next: [GDB/MI Output Records](GDB_002fMI-Output-Records.html#GDB_002fMI-Output-Records)]
:::

---

### 27.4 [GDB/MI]


The application which takes the MI output and presents the state of the program being debugged to the user is called a *front end*.

> 应用程序可以接受MI输出，并将调试程序的状态呈现给用户，称为前端。


Since [GDB/MI], changes to the MI interface may break existing usage. This section describes how the protocol changes and how to request previous version of the protocol when it does.

> 自[GDB/MI]以来，对MI接口的更改可能会破坏现有的使用情况。本节描述了协议的变化以及当发生变化时如何请求以前版本的协议。


Some changes in MI need not break a carefully designed front end, and for these the MI version will remain unchanged. The following is a list of changes that may occur within one level, so front ends should parse MI output in a way that can handle them:

> 一些对MI的更改并不会破坏精心设计的前端，因此MI版本将保持不变。以下是可能发生在同一级别的更改列表，因此前端应该以能处理它们的方式解析MI输出：

- New MI commands may be added.
- New fields may be added to the output of any MI command.

- The range of values for fields with specified values, e.g., `in_scope` (see [-var-update](GDB_002fMI-Variable-Objects.html#g_t_002dvar_002dupdate)) may be extended.

> 范围值可以扩展以指定值，例如`in_scope`（参见[-var-update](GDB_002fMI-Variable-Objects.html#g_t_002dvar_002dupdate)）。


If the changes are likely to break front ends, the MI version level will be increased by one. The new versions of the MI protocol are not compatible with the old versions. Old versions of MI remain available, allowing front ends to keep using them until they are modified to use the latest MI version.

> 如果这些变化可能破坏前端，MI 版本级别将提高一个。新版本的MI协议与旧版本不兼容。旧版本的MI仍然可用，允许前端继续使用它们，直到它们被修改为使用最新的MI版本。


Since `--interpreter=mi` always points to the latest MI version, it is recommended that front ends request a specific version of MI when launching [GDB] (e.g. `--interpreter=mi2`) to make sure they get an interpreter with the MI version they expect.

> 由于`--interpreter=mi`总是指向最新的MI版本，因此建议前端在启动[GDB]时请求一个特定的MI版本（例如`--interpreter=mi2`），以确保他们获得他们期望的MI版本的解释器。


The following table gives a summary of the released versions of the MI interface: the version number, the version of GDB in which it first appeared and the breaking changes compared to the previous version.

> 以下表格总结了MI接口的发布版本：版本号、首次出现的GDB版本以及与上一版本的重大变化。

+-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| MI version            | GDB version           | Breaking changes                                                                                                                                                                                                                                                                                               |
+=======================+=======================+================================================================================================================================================================================================================================================================================================================+
| :::   | None                                                                                                                                                                                                                                                                                                           |
| 1                     | 5.1                   |                                                                                                                                                                                                                                                                                                                |
| :::                   | :::                   |                                                                                                                                                                                                                                                                                                                |
+-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| :::   | -   The `-environment-pwd`, `-environment-directory` and `-environment-path` commands now returns values using the MI output syntax, rather than CLI output syntax.                                                                                                                                            |
| 2                     | 6.0                   | -   `-var-list-children`'s `children` result field is now a list, rather than a tuple.                                                                                                                                                                                                                         |
| :::                   | :::                   | -   `-var-update`'s `changelist` result field is now a list, rather than a tuple.                                                                                                                                                                                                                              |
+-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| :::   | -   The output of information about multi-location breakpoints has changed in the responses to the `-break-insert` and `-break-info` commands, as well as in the `=breakpoint-created` and `=breakpoint-modified` events. The multiple locations are now placed in a `locations` field, whose value is a list. |
| 3                     | 9.1                   |                                                                                                                                                                                                                                                                                                                |
| :::                   | :::                   |                                                                                                                                                                                                                                                                                                                |
+-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| :::   | -   The syntax of the \"script\" field in breakpoint output has changed in the responses to the `-break-insert` and `-break-info` commands, as well as the `=breakpoint-created` and `=breakpoint-modified` events. The previous output was syntactically invalid. The new output is a list.                   |
| 4                     | 13.1                  |                                                                                                                                                                                                                                                                                                                |
| :::                   | :::                   |                                                                                                                                                                                                                                                                                                                |
+-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+


If your front end cannot yet migrate to a more recent version of the MI protocol, you can nevertheless selectively enable specific features available in those recent MI versions, using the following commands:

> 如果您的前端尚未迁移到更新版本的MI协议，您仍然可以使用以下命令选择性地启用这些最新MI版本中可用的特性：

`-fix-multi-location-breakpoint-output`


:   Use the output for multi-location breakpoints which was introduced by MI 3, even when using MI versions below 3. This command has no effect when using MI version 3 or later.

> 使用MI 3引入的多位置断点输出，即使使用低于MI 3版本的也可以。当使用MI 3版本或更高版本时，此命令不起作用。

`-fix-breakpoint-script-output`


:   Use the output for the breakpoint \"script\" field which was introduced by MI 4, even when using MI versions below 4. This command has no effect when using MI version 4 or later.

> 使用MI 4引入的断点“脚本”字段的输出，即使在使用MI版本低于4的情况下也是如此。当使用MI版本4或更高版本时，此命令不起作用。


The best way to avoid unexpected changes in MI that might break your front end is to make your project known to [GDB]

> 最好的方法是避免MI中可能破坏您的前端的意外变化，就是让您的项目与GDB熟知。

---

::: header
Next: [GDB/MI Output Records](GDB_002fMI-Output-Records.html#GDB_002fMI-Output-Records)]
:::
