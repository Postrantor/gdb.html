---
tip: translate by openai@2023-06-23 21:44:04
...
---
description: GDB/MI Async Records (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: GDB/MI Async Records (Debugging with GDB)
lang: en
resource-type: document
title: GDB/MI Async Records (Debugging with GDB)
---
::: header
Next: [GDB/MI Breakpoint Information](GDB_002fMI-Breakpoint-Information.html#GDB_002fMI-Breakpoint-Information)]
:::

---

#### 27.5.3 [GDB/MI]


*Async* records are used to notify the [GDB/MI] commands (e.g., a breakpoint modified) or a result of target activity (e.g., target stopped).

> *异步*记录用于通知[GDB/MI]命令（例如，修改断点）或目标活动的结果（例如，目标停止）。

The following is the list of possible async records:

`*running,thread-id="thread"`


:   The target is now running. The `thread` may emit this notification several times, either for different threads, because it cannot resume all threads together, or even for a single thread, if the thread must be stepped though some code before letting it run freely.

> 目标现在正在运行。线程可能会多次发出此通知，要么是因为它无法同时恢复所有线程，要么是因为线程在自由运行之前必须先逐行检查一些代码。

`*stopped,reason="reason",thread-id="id",stopped-threads="stopped",core="core"`


:   The target has stopped. The `reason` field can have one of the following values:

> 目标已停止。`原因`字段可以有以下值之一：

```
`breakpoint-hit`

:   A breakpoint was reached.

`watchpoint-trigger`

:   A watchpoint was triggered.

`read-watchpoint-trigger`

:   A read watchpoint was triggered.

`access-watchpoint-trigger`

:   An access watchpoint was triggered.

`function-finished`

:   An -exec-finish or similar CLI command was accomplished.

`location-reached`

:   An -exec-until or similar CLI command was accomplished.

`watchpoint-scope`

:   A watchpoint has gone out of scope.

`end-stepping-range`

:   An -exec-next, -exec-next-instruction, -exec-step, -exec-step-instruction or similar CLI command was accomplished.

`exited-signalled`

:   The inferior exited because of a signal.

`exited`

:   The inferior exited.

`exited-normally`

:   The inferior exited normally.

`signal-received`

:   A signal was received by the inferior.

`solib-event`

:   The inferior has stopped due to a library being loaded or unloaded. This can happen when `stop-on-solib-events` (see [Files](Files.html#Files)) is set or when a `catch load` or `catch unload` catchpoint is in use (see [Set Catchpoints](Set-Catchpoints.html#Set-Catchpoints)).

`fork`

:   The inferior has forked. This is reported when `catch fork` (see [Set Catchpoints](Set-Catchpoints.html#Set-Catchpoints)) has been used.

`vfork`

:   The inferior has vforked. This is reported in when `catch vfork` (see [Set Catchpoints](Set-Catchpoints.html#Set-Catchpoints)) has been used.

`syscall-entry`

:   The inferior entered a system call. This is reported when `catch syscall` (see [Set Catchpoints](Set-Catchpoints.html#Set-Catchpoints)) has been used.

`syscall-return`

:   The inferior returned from a system call. This is reported when `catch syscall` (see [Set Catchpoints](Set-Catchpoints.html#Set-Catchpoints)) has been used.

`exec`

:   The inferior called `exec`. This is reported when `catch exec` (see [Set Catchpoints](Set-Catchpoints.html#Set-Catchpoints)) has been used.

`no-history`

:   There isn't enough history recorded to continue reverse execution.

The `id` field reports the processor core on which the stop event has happened. This field may be absent if such information is not available.
```

`=thread-group-added,id="id"`
`=thread-group-removed,id="id"`


:   A thread group was either added or removed. The `id` identifier of the thread group. When a thread group is added, it generally might not be associated with a running process. When a thread group is removed, its id becomes invalid and cannot be used in any way.

> 一个线程组已经被添加或者删除。线程组的`id`标识符。当线程组被添加时，它通常不会与正在运行的进程相关联。当线程组被删除时，它的id变得无效，不能以任何方式使用。

`=thread-group-started,id="id",pid="pid"`


:   A thread group became associated with a running program, either because the program was just started or the thread group was attached to a program. The `id` field contains process identifier, specific to the operating system.

> 一个线程组与一个正在运行的程序相关联，无论是因为程序刚刚启动还是线程组附加到程序上。`id`字段包含特定于操作系统的进程标识符。

`=thread-group-exited,id="id"[,exit-code="code"]`


:   A thread group is no longer associated with a running program, either because the program has exited, or because it was detached from. The `id` field is the exit code of the inferior; it exists only when the inferior exited with some code.

> 一个线程组不再与正在运行的程序相关联，因为程序已经退出或者已经被分离。`id`字段是下级的退出代码；它只存在于下级以某种代码退出时。

`=thread-created,id="id",group-id="gid"`
`=thread-exited,id="id",group-id="gid"`


:   A thread either was created, or has exited. The `id` field identifies the thread group this thread belongs to.

> 一个线程要么是创建的，要么已经退出。`id`字段标识了该线程属于哪个线程组。

`=thread-selected,id="id"[,frame="frame"]`


:   Informs that the selected thread or frame were changed. This notification is not emitted as result of the `-thread-select` or `-stack-select-frame` commands, but is emitted whenever an MI command that is not documented to change the selected thread and frame actually changes them. In particular, invoking, directly or indirectly (via user-defined command), the CLI `thread` or `frame` commands, will generate this notification. Changing the thread or frame from another user interface (see [Interpreters](Interpreters.html#Interpreters)) will also generate this notification.

> 通知已选择的线程或帧已更改。此通知不是作为`-thread-select`或`-stack-select-frame`命令的结果发出的，而是在不文档化更改所选择的线程和帧的MI命令实际更改它们时发出的。特别是，直接或间接（通过用户定义的命令）调用CLI `thread`或`frame`命令将生成此通知。从另一个用户界面（参见[解释器]（Interpreters.html#Interpreters））更改线程或帧也将生成此通知。

```
The `frame` field is only present if the newly selected thread is stopped. See [GDB/MI Frame Information](GDB_002fMI-Frame-Information.html#GDB_002fMI-Frame-Information) for the format of its value.

We suggest that in response to this notification, front ends highlight the selected thread and cause subsequent commands to apply to that thread.
```

`=library-loaded,...`


:   Reports that a new library file was loaded by the program. This notification has 5 fields---`id` field specifies the ranges of addresses belonging to this library.

> 报告程序加载了一个新的库文件。此通知具有5个字段---`id`字段指定属于此库的地址范围。

`=library-unloaded,...`


:   Reports that a library was unloaded by the program. This notification has 3 fields---`id` field, if present, specifies the id of the thread group in whose context the library was unloaded. If the field is absent, it means the library was unloaded in the context of all present thread groups.

> 报告程序卸载了一个库。此通知具有3个字段--如果存在`id`字段，则指定库卸载时的线程组的id。如果该字段缺失，则意味着库在所有现有线程组的上下文中被卸载。

`=traceframe-changed,num=tfnum,tracepoint=tpnum`
`=traceframe-changed,end`


:   Reports that the trace frame was changed and its new number is `tfnum`.

> 报告说跟踪框架已经改变，它的新编号是`tfnum`。

`=tsv-created,name=name,initial=initial`

:   Reports that the new trace state variable `name`.

`=tsv-deleted,name=name`
`=tsv-deleted`


:   Reports that the trace state variable `name` is deleted or all trace state variables are deleted.

> 报告说追踪状态变量`name`已被删除或者所有追踪状态变量都已被删除。

`=tsv-modified,name=name,initial=initial[,current=current]`


:   Reports that the trace state variable `name` of trace state variable is optional and is reported if the current value of trace state variable is known.

> 报告称，跟踪状态变量`name`是可选的，如果当前跟踪状态变量的值已知，则会报告。

`=breakpoint-created,bkpt=`
`=breakpoint-modified,bkpt=`
`=breakpoint-deleted,id=number`


:   Reports that a breakpoint was created, modified, or deleted, respectively. Only user-visible breakpoints are reported to the MI user.

> 报告已创建、修改或删除断点，仅向MI用户报告可见的断点。

```
The `bkpt` is the ordinal number of the breakpoint.

Note that if a breakpoint is emitted in the result record of a command, then it will not also be emitted in an async record.
```

`=record-started,thread-group="id",method="method"[,format="format"]`
`=record-stopped,thread-group="id"`


:   Execution log recording was either started or stopped on an inferior. The `id` identifier of the thread group corresponding to the affected inferior.

> 执行日志记录已在下级上启动或停止。与受影响下级相对应的`id`标识符线程组。

```
The `method` will be present and contain the currently used format. See [Process Record and Replay](Process-Record-and-Replay.html#Process-Record-and-Replay), for existing method and format values.
```

`=cmd-param-changed,param=param,value=value`


:   Reports that a parameter of the command `set param` is changed to `value` is `on`.

> 报告称命令'set param'的参数已更改为'value'为'on'。

`=memory-changed,thread-group=id,addr=addr,len=len[,type="code"]`


:   Reports that bytes from `addr` is the identifier of the thread group corresponding to the affected inferior. The optional `type="code"` part is reported if the memory written to holds executable code.

> 报告称来自`addr`的字节是与受影响的下级相对应的线程组的标识符。如果写入的内存包含可执行代码，则可选的`type="code"`部分将被报告。

---

::: header
Next: [GDB/MI Breakpoint Information](GDB_002fMI-Breakpoint-Information.html#GDB_002fMI-Breakpoint-Information)]
:::
