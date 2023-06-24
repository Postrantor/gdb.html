---
tip: translate by openai@2023-06-23 20:53:19
...
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

> [GDB]提供了一个通用的事件设施，因此Python代码可以被通知各种状态的变化，特别是在次要变化中发生的变化。


An *event* is just an object that describes some state change. The type of the object and its attributes will vary depending on the details of the change. All the existing events are described below.

> 事件只是描述某种状态变化的对象。对象的类型和属性将根据变化的细节而变化。以下描述了所有现有的事件。


In order to be notified of an event, you must register an event handler with an *event registry*. An event registry is an object in the `gdb.events` module which dispatches particular events. A registry provides methods to register and unregister event handlers:

> 要收到事件通知，您必须在*事件注册表*中注册事件处理程序。事件注册表是gdb.events模块中的一个对象，用于分发特定事件。注册表提供注册和取消注册事件处理程序的方法：

Function: **EventRegistry.connect** *(object)*


:   Add the given callable `object` to the registry. This object will be called when an event corresponding to this registry occurs.

> 将给定的可调用对象添加到注册表中。当与此注册表相对应的事件发生时，将调用此对象。

```
<!-- -->
```

Function: **EventRegistry.disconnect** *(object)*


:   Remove the given `object` from the registry. Once removed, the object will no longer receive notifications of events.

> 从注册表中移除给定的`对象`。一旦移除，该对象将不再收到事件的通知。

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

> 在上面的例子中，我们将处理程序`exit_handler`连接到注册表`events.exited`。一旦连接，当次级退出时就会调用`exit_handler`。这个例子中的参数*event*的类型是`gdb.ExitedEvent`。正如您在示例中所看到的，`ExitedEvent`对象具有一个属性，指示次级的退出代码。


Some events can be thread specific when [GDB] is running in non-stop mode. When represented in Python, these events all extend `gdb.ThreadEvent`. This event is a base class and is never emitted directly; instead, events which are emitted by this or other modules might extend this event. Examples of these events are `gdb.BreakpointEvent` and `gdb.ContinueEvent`. `gdb.ThreadEvent` holds the following attributes:

> 当[GDB]处于非停止模式时，某些事件可以是特定线程。在Python中表示时，这些事件都扩展了`gdb.ThreadEvent`。此事件是基类，不会直接发出；相反，由此或其他模块发出的事件可能会扩展此事件。这些事件的示例是`gdb.BreakpointEvent`和`gdb.ContinueEvent`。 `gdb.ThreadEvent`具有以下属性：

Variable: **ThreadEvent.inferior_thread**


:   In non-stop mode this attribute will be set to the specific thread which was involved in the emitted event. Otherwise, it will be set to `None`.

> 在非停止模式下，此属性将被设置为参与发出事件的特定线程。否则，它将被设置为“None”。


The following is a listing of the event registries that are available and details of the events they emit:

> 以下是可用的事件注册表列表及其发出事件的详细信息：

`events.cont`


:   Emits `gdb.ContinueEvent`, which extends `gdb.ThreadEvent`. This event indicates that the inferior has been continued after a stop. For inherited attribute refer to `gdb.ThreadEvent` above.

> 发出继承自`gdb.ThreadEvent`的`gdb.ContinueEvent`事件，表示下位机在停止后被继续执行。参见上面的`gdb.ThreadEvent`了解继承属性。

`events.exited`


:   Emits `events.ExitedEvent`, which indicates that the inferior has exited. `events.ExitedEvent` has two attributes:

> 发出`events.ExitedEvent`，表明下级已退出。`events.ExitedEvent`有两个属性：

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

> 发出`gdb.NewObjFileEvent`，表明[GDB]已加载了一个新的对象文件。`gdb.NewObjFileEvent`有一个属性：

```
Variable: **NewObjFileEvent.new_objfile**

:   A reference to the object file (`gdb.Objfile`) which has been loaded. See [Objfiles In Python](Objfiles-In-Python.html#Objfiles-In-Python), for details of the `gdb.Objfile` object.
```

`events.free_objfile`


:   Emits `gdb.FreeObjFileEvent` which indicates that an object file is about to be removed from [GDB]. One reason this can happen is when the inferior calls `dlclose`. `gdb.FreeObjFileEvent` has one attribute:

> 发出`gdb.FreeObjFileEvent`，表明一个对象文件即将从[GDB]中删除。这种情况发生的一个原因是当下属调用`dlclose`时。`gdb.FreeObjFileEvent`有一个属性：

```
Variable: **NewObjFileEvent.objfile**

:   A reference to the object file (`gdb.Objfile`) which will be unloaded. See [Objfiles In Python](Objfiles-In-Python.html#Objfiles-In-Python), for details of the `gdb.Objfile` object.
```

`events.clear_objfiles`


:   Emits `gdb.ClearObjFilesEvent` which indicates that the list of object files for a program space has been reset. `gdb.ClearObjFilesEvent` has one attribute:

> 发出`gdb.ClearObjFilesEvent`，表明一个程序空间的对象文件列表已重置。 `gdb.ClearObjFilesEvent`有一个属性：

```
Variable: **ClearObjFilesEvent.progspace**

:   A reference to the program space (`gdb.Progspace`) whose objfile list has been cleared. See [Progspaces In Python](Progspaces-In-Python.html#Progspaces-In-Python).
```

`events.inferior_call`


:   Emits events just before and after a function in the inferior is called by [GDB]. Before an inferior call, this emits an event of type `gdb.InferiorCallPreEvent`, and after an inferior call, this emits an event of type `gdb.InferiorCallPostEvent`.

> 此功能在[GDB]调用函数之前和之后发出事件。在下级调用之前，它会发出类型为“gdb.InferiorCallPreEvent”的事件，在下级调用之后，它会发出类型为“gdb.InferiorCallPostEvent”的事件。

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

> GDB用户通过`set *addr = value`等命令修改了下级内存，将发出`gdb.MemoryChangedEvent`事件。该事件具有以下属性：

Variable: **MemoryChangedEvent.address**

:   The start address of the changed region.

```
<!-- -->
```

Variable: **MemoryChangedEvent.length**

:   Length in bytes of the changed region.

`events.register_changed`


Emits `gdb.RegisterChangedEvent` which indicates that a register in the inferior has been modified by the [GDB] user.

> 它会发出`gdb.RegisterChangedEvent`事件，表明GDB用户已经修改了下属的寄存器。

Variable: **RegisterChangedEvent.frame**


:   A gdb.Frame object representing the frame in which the register was modified.

> 一个gdb.Frame对象，代表着修改寄存器的帧。

```
<!-- -->
```

Variable: **RegisterChangedEvent.regnum**

:   Denotes which register was modified.

`events.breakpoint_created`


This is emitted when a new breakpoint has been created. The argument that is passed is the new `gdb.Breakpoint` object.

> 这是在创建新断点时发出的。传递的参数是新的`gdb.Breakpoint`对象。

`events.breakpoint_modified`


This is emitted when a breakpoint has been modified in some way. The argument that is passed is the new `gdb.Breakpoint` object.

> 这是在某种方式修改断点时发出的。传递的参数是新的`gdb.Breakpoint`对象。

`events.breakpoint_deleted`


This is emitted when a breakpoint has been deleted. The argument that is passed is the `gdb.Breakpoint` object. When this event is emitted, the `gdb.Breakpoint` object will already be in its invalid state; that is, the `is_valid` method will return `False`.

> 这是在删除断点时发出的。传递的参数是`gdb.Breakpoint`对象。当发出此事件时，`gdb.Breakpoint`对象将处于无效状态；也就是说，`is_valid`方法将返回`False`。

`events.before_prompt`


This event carries no payload. It is emitted each time [GDB] presents a prompt to the user.

> 这个事件没有附带任何有效负载。每次[GDB]向用户提供提示时，都会发出这个事件。

`events.new_inferior`


This is emitted when a new inferior is created. Note that the inferior is not necessarily running; in fact, it may not even have an associated executable.

> 这是在创建新的次级对象时发出的。请注意，次级对象不一定正在运行；事实上，它甚至可能没有相关的可执行文件。

The event is of type `gdb.NewInferiorEvent`. This has a single attribute:

Variable: **NewInferiorEvent.inferior**

:   The new inferior, a `gdb.Inferior` object.

`events.inferior_deleted`


This is emitted when an inferior has been deleted. Note that this is not the same as process exit; it is notified when the inferior itself is removed, say via `remove-inferiors`.

> 这是在删除次级对象时发出的。请注意，这与进程退出不同；它是在次级对象本身被移除时通知的，比如通过`remove-inferiors`。


The event is of type `gdb.InferiorDeletedEvent`. This has a single attribute:

> 此事件的类型为gdb.InferiorDeletedEvent，它只有一个属性。

Variable: **InferiorDeletedEvent.inferior**

:   The inferior that is being removed, a `gdb.Inferior` object.

`events.new_thread`


This is emitted when [GDB] notices a new thread. The event is of type `gdb.NewThreadEvent`, which extends `gdb.ThreadEvent`. This has a single attribute:

> 这在[GDB]注意到新线程时发出。该事件的类型是`gdb.NewThreadEvent`，它继承自`gdb.ThreadEvent`。它有一个属性：

Variable: **NewThreadEvent.inferior_thread**

:   The new thread.

`events.thread_exited`


This is emitted when [GDB] notices a thread has exited. The event is of type `gdb.ThreadExitedEvent` which extends `gdb.ThreadEvent`. This has a single attribute:

> 当GDB注意到一个线程已退出时，就会发出这个事件。该事件的类型是`gdb.ThreadExitedEvent`，它继承自`gdb.ThreadEvent`。它只有一个属性：

Variable: **ThreadExitedEvent.inferior_thread**

:   The exiting thread.

`events.gdb_exiting`


This is emitted when [GDB] exits as a result of an internal error, or after an unexpected signal. The event is of type `gdb.GdbExitingEvent`, which has a single attribute:

> 当GDB由于内部错误或意外信号而退出时，就会发出此事件。该事件的类型为`gdb.GdbExitingEvent`，具有一个属性：

Variable: **GdbExitingEvent.exit_code**

:   An integer, the value of the exit code [GDB] will return.

`events.connection_removed`


This is emitted when [GDB] removes a connection (see [Connections In Python](Connections-In-Python.html#Connections-In-Python)). The event is of type `gdb.ConnectionEvent`. This has a single read-only attribute:

> 这是在[GDB]删除连接时发出的（请参阅[Python中的连接]（Connections-In-Python.html#Connections-In-Python））。该事件的类型为`gdb.ConnectionEvent`。它有一个只读属性：

Variable: **ConnectionEvent.connection**

:   The `gdb.TargetConnection` that is being removed.

---

::: header
Next: [Threads In Python](Threads-In-Python.html#Threads-In-Python)]
:::
