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

Since [GDB/MI], changes to the MI interface may break existing usage. This section describes how the protocol changes and how to request previous version of the protocol when it does.

Some changes in MI need not break a carefully designed front end, and for these the MI version will remain unchanged. The following is a list of changes that may occur within one level, so front ends should parse MI output in a way that can handle them:

- New MI commands may be added.
- New fields may be added to the output of any MI command.
- The range of values for fields with specified values, e.g., `in_scope` (see [-var-update](GDB_002fMI-Variable-Objects.html#g_t_002dvar_002dupdate)) may be extended.

If the changes are likely to break front ends, the MI version level will be increased by one. The new versions of the MI protocol are not compatible with the old versions. Old versions of MI remain available, allowing front ends to keep using them until they are modified to use the latest MI version.

Since `--interpreter=mi` always points to the latest MI version, it is recommended that front ends request a specific version of MI when launching [GDB] (e.g. `--interpreter=mi2`) to make sure they get an interpreter with the MI version they expect.

The following table gives a summary of the released versions of the MI interface: the version number, the version of GDB in which it first appeared and the breaking changes compared to the previous version.

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

`-fix-multi-location-breakpoint-output`

:   Use the output for multi-location breakpoints which was introduced by MI 3, even when using MI versions below 3. This command has no effect when using MI version 3 or later.

`-fix-breakpoint-script-output`

:   Use the output for the breakpoint \"script\" field which was introduced by MI 4, even when using MI versions below 4. This command has no effect when using MI version 4 or later.

The best way to avoid unexpected changes in MI that might break your front end is to make your project known to [GDB]

---

::: header
Next: [GDB/MI Output Records](GDB_002fMI-Output-Records.html#GDB_002fMI-Output-Records)]
:::
