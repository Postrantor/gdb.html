---
description: Events In Python (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Events In Python (Debugging with GDB)
lang: en
resource-type: document
title: Events In Python (Debugging with GDB)
---
::: header
Next: [Threads In Python](Threads-In-Python.html#Threads-In-Python)]
:::

---

#### 23.3.2.17 Events In Python

[GDB] provides a general event facility so that Python code can be notified of various state changes, particularly changes that occur in the inferior.

An *event* is just an object that describes some state change. The type of the object and its attributes will vary depending on the details of the change. All the existing events are described below.

In order to be notified of an event, you must register an event handler with an *event registry*. An event registry is an object in the `gdb.events` module which dispatches particular events. A registry provides methods to register and unregister event handlers:

Function: **EventRegistry.connect** *(object)*

:   Add the given callable `object` to the registry. This object will be called when an event corresponding to this registry occurs.

```
<!-- -->
```

Function: **EventRegistry.disconnect** *(object)*

:   Remove the given `object` from the registry. Once removed, the object will no longer receive notifications of events.

Here is an example:

::: smallexample

```bash
def exit_handler (event):
    print ("event type: exit")
    if hasattr (event, 'exit_code'):
        print ("exit code: %d" % (event.exit_code))
    else:
        print ("exit code not available")

gdb.events.exited.connect (exit_handler)
```

:::

In the above example we connect our handler `exit_handler` to the registry `events.exited`. Once connected, `exit_handler` gets called when the inferior exits. The argument *event* in this example is of type `gdb.ExitedEvent`. As you can see in the example the `ExitedEvent` object has an attribute which indicates the exit code of the inferior.

Some events can be thread specific when [GDB] is running in non-stop mode. When represented in Python, these events all extend `gdb.ThreadEvent`. This event is a base class and is never emitted directly; instead, events which are emitted by this or other modules might extend this event. Examples of these events are `gdb.BreakpointEvent` and `gdb.ContinueEvent`. `gdb.ThreadEvent` holds the following attributes:

Variable: **ThreadEvent.inferior_thread**

:   In non-stop mode this attribute will be set to the specific thread which was involved in the emitted event. Otherwise, it will be set to `None`.

The following is a listing of the event registries that are available and details of the events they emit:

`events.cont`

:   Emits `gdb.ContinueEvent`, which extends `gdb.ThreadEvent`. This event indicates that the inferior has been continued after a stop. For inherited attribute refer to `gdb.ThreadEvent` above.

`events.exited`

:   Emits `events.ExitedEvent`, which indicates that the inferior has exited. `events.ExitedEvent` has two attributes:

```
Variable: **ExitedEvent.exit_code**

:   An integer representing the exit code, if available, which the inferior has returned. (The exit code could be unavailable if, for example, [GDB] detaches from the inferior.) If the exit code is unavailable, the attribute does not exist.

Variable: **ExitedEvent.inferior**

:   A reference to the inferior which triggered the `exited` event.
```

`events.stop`

:   Emits `gdb.StopEvent`, which extends `gdb.ThreadEvent`.

```
Indicates that the inferior has stopped. All events emitted by this registry extend `gdb.StopEvent`. As a child of `gdb.ThreadEvent`, `gdb.StopEvent` will indicate the stopped thread when [GDB] is running in non-stop mode. Refer to `gdb.ThreadEvent` above for more details.

Emits `gdb.SignalEvent`, which extends `gdb.StopEvent`.

This event indicates that the inferior or one of its threads has received a signal. `gdb.SignalEvent` has the following attributes:

Variable: **SignalEvent.stop_signal**

:   A string representing the signal received by the inferior. A list of possible signal values can be obtained by running the command `info signals` in the [GDB] command prompt.

Also emits `gdb.BreakpointEvent`, which extends `gdb.StopEvent`.

`gdb.BreakpointEvent` event indicates that one or more breakpoints have been hit, and has the following attributes:

Variable: **BreakpointEvent.breakpoints**

:   A sequence containing references to all the breakpoints (type `gdb.Breakpoint`) that were hit. See [Breakpoints In Python](Breakpoints-In-Python.html#Breakpoints-In-Python), for details of the `gdb.Breakpoint` object.

Variable: **BreakpointEvent.breakpoint**

:   A reference to the first breakpoint that was hit. This attribute is maintained for backward compatibility and is now deprecated in favor of the `gdb.BreakpointEvent.breakpoints` attribute.
```

`events.new_objfile`

:   Emits `gdb.NewObjFileEvent` which indicates that a new object file has been loaded by [GDB]. `gdb.NewObjFileEvent` has one attribute:

```
Variable: **NewObjFileEvent.new_objfile**

:   A reference to the object file (`gdb.Objfile`) which has been loaded. See [Objfiles In Python](Objfiles-In-Python.html#Objfiles-In-Python), for details of the `gdb.Objfile` object.
```

`events.free_objfile`

:   Emits `gdb.FreeObjFileEvent` which indicates that an object file is about to be removed from [GDB]. One reason this can happen is when the inferior calls `dlclose`. `gdb.FreeObjFileEvent` has one attribute:

```
Variable: **NewObjFileEvent.objfile**

:   A reference to the object file (`gdb.Objfile`) which will be unloaded. See [Objfiles In Python](Objfiles-In-Python.html#Objfiles-In-Python), for details of the `gdb.Objfile` object.
```

`events.clear_objfiles`

:   Emits `gdb.ClearObjFilesEvent` which indicates that the list of object files for a program space has been reset. `gdb.ClearObjFilesEvent` has one attribute:

```
Variable: **ClearObjFilesEvent.progspace**

:   A reference to the program space (`gdb.Progspace`) whose objfile list has been cleared. See [Progspaces In Python](Progspaces-In-Python.html#Progspaces-In-Python).
```

`events.inferior_call`

:   Emits events just before and after a function in the inferior is called by [GDB]. Before an inferior call, this emits an event of type `gdb.InferiorCallPreEvent`, and after an inferior call, this emits an event of type `gdb.InferiorCallPostEvent`.

:

`gdb.InferiorCallPreEvent`

:   Indicates that a function in the inferior is about to be called.

```
Variable: **InferiorCallPreEvent.ptid**

:   The thread in which the call will be run.

Variable: **InferiorCallPreEvent.address**

:   The location of the function to be called.


```

`gdb.InferiorCallPostEvent`

:   Indicates that a function in the inferior has just been called.

```
Variable: **InferiorCallPostEvent.ptid**

:   The thread in which the call was run.

Variable: **InferiorCallPostEvent.address**

:   The location of the function that was called.
```

`events.memory_changed`

Emits `gdb.MemoryChangedEvent` which indicates that the memory of the inferior has been modified by the [GDB] user, for instance via a command like `set *addr = value`. The event has the following attributes:

Variable: **MemoryChangedEvent.address**

:   The start address of the changed region.

```
<!-- -->
```

Variable: **MemoryChangedEvent.length**

:   Length in bytes of the changed region.

`events.register_changed`

Emits `gdb.RegisterChangedEvent` which indicates that a register in the inferior has been modified by the [GDB] user.

Variable: **RegisterChangedEvent.frame**

:   A gdb.Frame object representing the frame in which the register was modified.

```
<!-- -->
```

Variable: **RegisterChangedEvent.regnum**

:   Denotes which register was modified.

`events.breakpoint_created`

This is emitted when a new breakpoint has been created. The argument that is passed is the new `gdb.Breakpoint` object.

`events.breakpoint_modified`

This is emitted when a breakpoint has been modified in some way. The argument that is passed is the new `gdb.Breakpoint` object.

`events.breakpoint_deleted`

This is emitted when a breakpoint has been deleted. The argument that is passed is the `gdb.Breakpoint` object. When this event is emitted, the `gdb.Breakpoint` object will already be in its invalid state; that is, the `is_valid` method will return `False`.

`events.before_prompt`

This event carries no payload. It is emitted each time [GDB] presents a prompt to the user.

`events.new_inferior`

This is emitted when a new inferior is created. Note that the inferior is not necessarily running; in fact, it may not even have an associated executable.

The event is of type `gdb.NewInferiorEvent`. This has a single attribute:

Variable: **NewInferiorEvent.inferior**

:   The new inferior, a `gdb.Inferior` object.

`events.inferior_deleted`

This is emitted when an inferior has been deleted. Note that this is not the same as process exit; it is notified when the inferior itself is removed, say via `remove-inferiors`.

The event is of type `gdb.InferiorDeletedEvent`. This has a single attribute:

Variable: **InferiorDeletedEvent.inferior**

:   The inferior that is being removed, a `gdb.Inferior` object.

`events.new_thread`

This is emitted when [GDB] notices a new thread. The event is of type `gdb.NewThreadEvent`, which extends `gdb.ThreadEvent`. This has a single attribute:

Variable: **NewThreadEvent.inferior_thread**

:   The new thread.

`events.thread_exited`

This is emitted when [GDB] notices a thread has exited. The event is of type `gdb.ThreadExitedEvent` which extends `gdb.ThreadEvent`. This has a single attribute:

Variable: **ThreadExitedEvent.inferior_thread**

:   The exiting thread.

`events.gdb_exiting`

This is emitted when [GDB] exits as a result of an internal error, or after an unexpected signal. The event is of type `gdb.GdbExitingEvent`, which has a single attribute:

Variable: **GdbExitingEvent.exit_code**

:   An integer, the value of the exit code [GDB] will return.

`events.connection_removed`

This is emitted when [GDB] removes a connection (see [Connections In Python](Connections-In-Python.html#Connections-In-Python)). The event is of type `gdb.ConnectionEvent`. This has a single read-only attribute:

Variable: **ConnectionEvent.connection**

:   The `gdb.TargetConnection` that is being removed.

---

::: header
Next: [Threads In Python](Threads-In-Python.html#Threads-In-Python)]
:::
