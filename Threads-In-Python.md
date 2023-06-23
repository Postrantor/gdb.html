---
description: Threads In Python (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Threads In Python (Debugging with GDB)
lang: en
resource-type: document
title: Threads In Python (Debugging with GDB)
---
::: header
Next: [Recordings In Python](Recordings-In-Python.html#Recordings-In-Python)]
:::

---

#### 23.3.2.18 Threads In Python

Python scripts can access information about, and manipulate inferior threads controlled by [GDB], via objects of the `gdb.InferiorThread` class.

The following thread-related functions are available in the `gdb` module:

Function: **gdb.selected_thread** *()*

:   This function returns the thread object for the selected thread. If there is no selected thread, this will return `None`.

To get the list of threads for an inferior, use the `Inferior.threads()` method. See [Inferiors In Python](Inferiors-In-Python.html#Inferiors-In-Python).

A `gdb.InferiorThread` object has the following attributes:

Variable: **InferiorThread.name**

:   The name of the thread. If the user specified a name using `thread name`, then this returns that name. Otherwise, if an OS-supplied name is available, then it is returned. Otherwise, this returns `None`.

```
This attribute can be assigned to. The new value must be a string object, which sets the new name, or `None`, which removes any user-specified thread name.
```

```
<!-- -->
```

Variable: **InferiorThread.num**

:   The per-inferior number of the thread, as assigned by GDB.

```
<!-- -->
```

Variable: **InferiorThread.global_num**

:   The global ID of the thread, as assigned by GDB. You can use this to make Python breakpoints thread-specific, for example (see [The Breakpoint.thread attribute](Breakpoints-In-Python.html#python_005fbreakpoint_005fthread)).

Variable: **InferiorThread.ptid**

:   ID of the thread, as assigned by the operating system. This attribute is a tuple containing three integers. The first is the Process ID (PID); the second is the Lightweight Process ID (LWPID), and the third is the Thread ID (TID). Either the LWPID or TID may be 0, which indicates that the operating system does not use that identifier.

```
<!-- -->
```

Variable: **InferiorThread.inferior**

:   The inferior this thread belongs to. This attribute is represented as a `gdb.Inferior` object. This attribute is not writable.

```
<!-- -->
```

Variable: **InferiorThread.details**

:   A string containing target specific thread state information. The format of this string varies by target. If there is no additional state information for this thread, then this attribute contains `None`.

```
For example, on a [GNU]'](General-Query-Packets.html#qThreadExtraInfo)).

[GDB]'](Threads.html#info_005fthreads)).
```

A `gdb.InferiorThread` object has the following methods:

Function: **InferiorThread.is_valid** *()*

:   Returns `True` if the `gdb.InferiorThread` object is valid, `False` if not. A `gdb.InferiorThread` object will become invalid if the thread exits, or the inferior that the thread belongs is deleted. All other `gdb.InferiorThread` methods will throw an exception if it is invalid at the time the method is called.

```
<!-- -->
```

Function: **InferiorThread.switch** *()*

:   This changes [GDB]'s currently selected thread to the one represented by this object.

```
<!-- -->
```

Function: **InferiorThread.is_stopped** *()*

:   Return a Boolean indicating whether the thread is stopped.

```
<!-- -->
```

Function: **InferiorThread.is_running** *()*

:   Return a Boolean indicating whether the thread is running.

```
<!-- -->
```

Function: **InferiorThread.is_exited** *()*

:   Return a Boolean indicating whether the thread is exited.

```
<!-- -->
```

Function: **InferiorThread.handle** *()*

:   Return the thread object's handle, represented as a Python `bytes` object. A `gdb.Value` representation of the handle may be constructed via `gdb.Value(bufobj, type)` where `bufobj` is a `gdb.Type` for the handle type.

---

::: header
Next: [Recordings In Python](Recordings-In-Python.html#Recordings-In-Python)]
:::
