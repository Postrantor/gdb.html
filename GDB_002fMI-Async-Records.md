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

The following is the list of possible async records:

`*running,thread-id="thread"`

:   The target is now running. The `thread` may emit this notification several times, either for different threads, because it cannot resume all threads together, or even for a single thread, if the thread must be stepped though some code before letting it run freely.

`*stopped,reason="reason",thread-id="id",stopped-threads="stopped",core="core"`

:   The target has stopped. The `reason` field can have one of the following values:

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

`=thread-group-started,id="id",pid="pid"`

:   A thread group became associated with a running program, either because the program was just started or the thread group was attached to a program. The `id` field contains process identifier, specific to the operating system.

`=thread-group-exited,id="id"[,exit-code="code"]`

:   A thread group is no longer associated with a running program, either because the program has exited, or because it was detached from. The `id` field is the exit code of the inferior; it exists only when the inferior exited with some code.

`=thread-created,id="id",group-id="gid"`
`=thread-exited,id="id",group-id="gid"`

:   A thread either was created, or has exited. The `id` field identifies the thread group this thread belongs to.

`=thread-selected,id="id"[,frame="frame"]`

:   Informs that the selected thread or frame were changed. This notification is not emitted as result of the `-thread-select` or `-stack-select-frame` commands, but is emitted whenever an MI command that is not documented to change the selected thread and frame actually changes them. In particular, invoking, directly or indirectly (via user-defined command), the CLI `thread` or `frame` commands, will generate this notification. Changing the thread or frame from another user interface (see [Interpreters](Interpreters.html#Interpreters)) will also generate this notification.

```
The `frame` field is only present if the newly selected thread is stopped. See [GDB/MI Frame Information](GDB_002fMI-Frame-Information.html#GDB_002fMI-Frame-Information) for the format of its value.

We suggest that in response to this notification, front ends highlight the selected thread and cause subsequent commands to apply to that thread.
```

`=library-loaded,...`

:   Reports that a new library file was loaded by the program. This notification has 5 fields---`id` field specifies the ranges of addresses belonging to this library.

`=library-unloaded,...`

:   Reports that a library was unloaded by the program. This notification has 3 fields---`id` field, if present, specifies the id of the thread group in whose context the library was unloaded. If the field is absent, it means the library was unloaded in the context of all present thread groups.

`=traceframe-changed,num=tfnum,tracepoint=tpnum`
`=traceframe-changed,end`

:   Reports that the trace frame was changed and its new number is `tfnum`.

`=tsv-created,name=name,initial=initial`

:   Reports that the new trace state variable `name`.

`=tsv-deleted,name=name`
`=tsv-deleted`

:   Reports that the trace state variable `name` is deleted or all trace state variables are deleted.

`=tsv-modified,name=name,initial=initial[,current=current]`

:   Reports that the trace state variable `name` of trace state variable is optional and is reported if the current value of trace state variable is known.

`=breakpoint-created,bkpt=`
`=breakpoint-modified,bkpt=`
`=breakpoint-deleted,id=number`

:   Reports that a breakpoint was created, modified, or deleted, respectively. Only user-visible breakpoints are reported to the MI user.

```
The `bkpt` is the ordinal number of the breakpoint.

Note that if a breakpoint is emitted in the result record of a command, then it will not also be emitted in an async record.
```

`=record-started,thread-group="id",method="method"[,format="format"]`
`=record-stopped,thread-group="id"`

:   Execution log recording was either started or stopped on an inferior. The `id` identifier of the thread group corresponding to the affected inferior.

```
The `method` will be present and contain the currently used format. See [Process Record and Replay](Process-Record-and-Replay.html#Process-Record-and-Replay), for existing method and format values.
```

`=cmd-param-changed,param=param,value=value`

:   Reports that a parameter of the command `set param` is changed to `value` is `on`.

`=memory-changed,thread-group=id,addr=addr,len=len[,type="code"]`

:   Reports that bytes from `addr` is the identifier of the thread group corresponding to the affected inferior. The optional `type="code"` part is reported if the memory written to holds executable code.

---

::: header
Next: [GDB/MI Breakpoint Information](GDB_002fMI-Breakpoint-Information.html#GDB_002fMI-Breakpoint-Information)]
:::
