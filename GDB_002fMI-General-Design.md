---
tip: translate by openai@2023-06-23 21:59:47
...
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

> 交互式[GDB/MI]状态，不能方便地与命令相关联，并作为该命令响应的一部分报告。

The important examples of notifications are:


- Exec notifications. These are used to report changes in target state---when a target is resumed, or stopped. It would not be feasible to include this information in response of resuming commands, because one resume commands can result in multiple events in different threads. Also, quite some time may pass before any event happens in the target, while a frontend needs to know whether the resuming command itself was successfully executed.

> -执行通知。这些用于报告目标状态的变化 - 当目标恢复或停止时。将此信息包含在恢复命令的响应中是不可行的，因为一个恢复命令可能会在不同的线程中导致多个事件。而且，在目标发生任何事件之前，可能需要相当长的时间，而前端需要知道恢复命令本身是否已成功执行。

- Console output, and status notifications. Console output notifications are used to report output of CLI commands, as well as diagnostics for other commands. Status notifications are used to report the progress of a long-running operation. Naturally, including this information in command response would mean no output is produced until the command is finished, which is undesirable.

> 控制台输出和状态通知。控制台输出通知用于报告CLI命令的输出以及其他命令的诊断信息。状态通知用于报告长时间运行操作的进度。当然，如果将此信息包含在命令响应中，则意味着在命令完成之前不会产生任何输出，这是不可取的。

- General notifications. Commands may have various side effects on the [GDB] or target state beyond their official purpose. For example, a command may change the selected thread. Although such changes can be included in command response, using notification allows for more orthogonal frontend design.

> 一般通知。命令可能会对[GDB]或目标状态产生各种副作用，超出其官方目的。例如，命令可能会更改所选择的线程。虽然可以将此类更改包括在命令响应中，但使用通知可以更加正交地设计前端。


There's no guarantee that whenever an MI command reports an error, [GDB] or the target are in any specific state, and especially, the state is not reverted to the state before the MI command was processed. Therefore, whenever an MI command results in an error, we recommend that the frontend refreshes all the information shown in the user interface.

> 没有保证每当MI命令报告错误时，[GDB]或目标处于任何特定状态，尤其是，状态不会恢复到MI命令处理之前的状态。因此，每当MI命令导致错误时，我们建议前端刷新用户界面中显示的所有信息。

---


• [Context management](Context-management.html#Context-management):                                                    

> •[上下文管理](Context-management.html#Context-management):

• [Asynchronous and non-stop modes](Asynchronous-and-non_002dstop-modes.html#Asynchronous-and-non_002dstop-modes):     

> •[异步和非停止模式](Asynchronous-and-non_002dstop-modes.html#Asynchronous-and-non_002dstop-modes):

• [Thread groups](Thread-groups.html#Thread-groups):                                                                   

> • [线程组](Thread-groups.html#Thread-groups):

---

---

::: header
Next: [GDB/MI Command Syntax](GDB_002fMI-Command-Syntax.html#GDB_002fMI-Command-Syntax)]
:::
