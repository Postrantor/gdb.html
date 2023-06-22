---
description: GDB/MI General Design (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: GDB/MI General Design (Debugging with GDB)
lang: en
resource-type: document
title: GDB/MI General Design (Debugging with GDB)
---
::: header
Next: [GDB/MI Command Syntax](GDB_002fMI-Command-Syntax.html#GDB_002fMI-Command-Syntax)]
:::

---

### 27.1 [GDB/MI]

Interaction of a [GDB/MI] state, that cannot conveniently be associated with a command and reported as part of that command response.

The important examples of notifications are:

- Exec notifications. These are used to report changes in target state---when a target is resumed, or stopped. It would not be feasible to include this information in response of resuming commands, because one resume commands can result in multiple events in different threads. Also, quite some time may pass before any event happens in the target, while a frontend needs to know whether the resuming command itself was successfully executed.
- Console output, and status notifications. Console output notifications are used to report output of CLI commands, as well as diagnostics for other commands. Status notifications are used to report the progress of a long-running operation. Naturally, including this information in command response would mean no output is produced until the command is finished, which is undesirable.
- General notifications. Commands may have various side effects on the [GDB] or target state beyond their official purpose. For example, a command may change the selected thread. Although such changes can be included in command response, using notification allows for more orthogonal frontend design.

There's no guarantee that whenever an MI command reports an error, [GDB] or the target are in any specific state, and especially, the state is not reverted to the state before the MI command was processed. Therefore, whenever an MI command results in an error, we recommend that the frontend refreshes all the information shown in the user interface.

---

• [Context management](Context-management.html#Context-management):                                                    
• [Asynchronous and non-stop modes](Asynchronous-and-non_002dstop-modes.html#Asynchronous-and-non_002dstop-modes):     
• [Thread groups](Thread-groups.html#Thread-groups):                                                                   

---

---

::: header
Next: [GDB/MI Command Syntax](GDB_002fMI-Command-Syntax.html#GDB_002fMI-Command-Syntax)]
:::
