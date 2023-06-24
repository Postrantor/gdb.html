---
tip: translate by openai@2023-06-24 03:55:57
...
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

> Python 脚本可以访问有关 [GDB] 控制的次级线程的信息，并通过 `gdb.InferiorThread` 类的对象来操纵它们。

The following thread-related functions are available in the `gdb` module:

Function: **gdb.selected_thread** *()*


:   This function returns the thread object for the selected thread. If there is no selected thread, this will return `None`.

> 这个函数返回所选线程的线程对象。如果没有选择的线程，它将返回`None`。


To get the list of threads for an inferior, use the `Inferior.threads()` method. See [Inferiors In Python](Inferiors-In-Python.html#Inferiors-In-Python).

> 要获取次等级的线程列表，请使用`Inferior.threads()`方法。参见[Python中的次等级](Inferiors-In-Python.html#Inferiors-In-Python)。

A `gdb.InferiorThread` object has the following attributes:

Variable: **InferiorThread.name**


:   The name of the thread. If the user specified a name using `thread name`, then this returns that name. Otherwise, if an OS-supplied name is available, then it is returned. Otherwise, this returns `None`.

> 线程的名称。如果用户使用“线程名称”指定了一个名称，那么这将返回该名称。否则，如果操作系统提供的名称可用，则返回该名称。否则，返回“无”。

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

> 线程的全局ID，由GDB指定。您可以使用它来使Python断点特定于线程，例如（请参阅[Breakpoint.thread属性](Breakpoints-In-Python.html#python_005fbreakpoint_005fthread))。

Variable: **InferiorThread.ptid**


:   ID of the thread, as assigned by the operating system. This attribute is a tuple containing three integers. The first is the Process ID (PID); the second is the Lightweight Process ID (LWPID), and the third is the Thread ID (TID). Either the LWPID or TID may be 0, which indicates that the operating system does not use that identifier.

> 线程的ID，由操作系统分配。此属性是一个包含三个整数的元组。第一个是进程ID（PID）；第二个是轻量级进程ID（LWPID），第三个是线程ID（TID）。LWPID或TID其中之一可能为0，这表示操作系统不使用该标识符。

```
<!-- -->
```

Variable: **InferiorThread.inferior**


:   The inferior this thread belongs to. This attribute is represented as a `gdb.Inferior` object. This attribute is not writable.

> 此线程属于的下级。此属性表示为`gdb.Inferior`对象。此属性不可写。

```
<!-- -->
```

Variable: **InferiorThread.details**


:   A string containing target specific thread state information. The format of this string varies by target. If there is no additional state information for this thread, then this attribute contains `None`.

> 一个包含目标特定线程状态信息的字符串。此字符串的格式因目标而异。如果此线程没有额外的状态信息，那么此属性包含“None”。

```
For example, on a [GNU]'](General-Query-Packets.html#qThreadExtraInfo)).

[GDB]'](Threads.html#info_005fthreads)).
```

A `gdb.InferiorThread` object has the following methods:

Function: **InferiorThread.is_valid** *()*


:   Returns `True` if the `gdb.InferiorThread` object is valid, `False` if not. A `gdb.InferiorThread` object will become invalid if the thread exits, or the inferior that the thread belongs is deleted. All other `gdb.InferiorThread` methods will throw an exception if it is invalid at the time the method is called.

> 如果gdb.InferiorThread对象有效，则返回True，如果无效，则返回False。如果线程退出或属于该线程的下级被删除，gdb.InferiorThread对象将变得无效。调用其他gdb.InferiorThread方法时，如果处于无效状态，则会抛出异常。

```
<!-- -->
```

Function: **InferiorThread.switch** *()*


:   This changes [GDB]'s currently selected thread to the one represented by this object.

> 这会更改 GDB 的当前选定线程为由此对象表示的线程。

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

> 返回线程对象的句柄，表示为Python字节对象。可以通过`gdb.Value(bufobj, type)`构造`gdb.Value`表示句柄，其中`bufobj`是句柄类型的`gdb.Type`。

---

::: header
Next: [Recordings In Python](Recordings-In-Python.html#Recordings-In-Python)]
:::
