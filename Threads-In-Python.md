---
tip: translate by openai@2023-06-23 14:30:08
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

> Python腳本可以通過`gdb.InferiorThread`類的對象訪問有關[GDB]控制的次要線程的信息，並進行操作。


The following thread-related functions are available in the `gdb` module:

> `gdb` 模块中提供以下与线程相关的函数：


Function: **gdb.selected_thread** *()*

> 功能：**gdb.selected_thread***（）*


:   This function returns the thread object for the selected thread. If there is no selected thread, this will return `None`.

> 这个函数返回所选线程的线程对象。如果没有选择线程，将返回`None`。


To get the list of threads for an inferior, use the `Inferior.threads()` method. See [Inferiors In Python](Inferiors-In-Python.html#Inferiors-In-Python).

> 要获取次级线程的列表，请使用`Inferior.threads()`方法。参见[Python中的次级](Inferiors-In-Python.html#Inferiors-In-Python)。


A `gdb.InferiorThread` object has the following attributes:

> 一个`gdb.InferiorThread`对象具有以下属性：


Variable: **InferiorThread.name**

> 变量：**InferiorThread.name**


:   The name of the thread. If the user specified a name using `thread name`, then this returns that name. Otherwise, if an OS-supplied name is available, then it is returned. Otherwise, this returns `None`.

> 线程的名称。如果用户使用“线程名称”指定了一个名称，那么它将返回该名称。否则，如果操作系统提供了一个名称，则返回该名称。否则，返回“None”。

```
This attribute can be assigned to. The new value must be a string object, which sets the new name, or `None`, which removes any user-specified thread name.
```

```

```


Variable: **InferiorThread.num**

> 变量：**InferiorThread.num**


:   The per-inferior number of the thread, as assigned by GDB.

> GDB分配的线程的每个次级号码。

```

```


Variable: **InferiorThread.global_num**

> 变量：**InferiorThread.global_num**


:   The global ID of the thread, as assigned by GDB. You can use this to make Python breakpoints thread-specific, for example (see [The Breakpoint.thread attribute](Breakpoints-In-Python.html#python_005fbreakpoint_005fthread)).

> 线程的全局ID，由GDB分配。您可以使用它来使Python断点特定于线程，例如（参见[断点.线程属性](Breakpoints-In-Python.html#python_005fbreakpoint_005fthread))。


Variable: **InferiorThread.ptid**

> 变量：**InferiorThread.ptid**


:   ID of the thread, as assigned by the operating system. This attribute is a tuple containing three integers. The first is the Process ID (PID); the second is the Lightweight Process ID (LWPID), and the third is the Thread ID (TID). Either the LWPID or TID may be 0, which indicates that the operating system does not use that identifier.

> 线程的ID，由操作系统分配。此属性是一个包含三个整数的元组。第一个是进程ID（PID）；第二个是轻量级进程ID（LWPID），第三个是线程ID（TID）。 LWPID或TID可以是0，表示操作系统不使用该标识符。

```

```


Variable: **InferiorThread.inferior**

> 变量：**InferiorThread.inferior**


:   The inferior this thread belongs to. This attribute is represented as a `gdb.Inferior` object. This attribute is not writable.

> 这个线程属于哪个次级？这个属性用`gdb.Inferior`对象表示。这个属性是不可写的。

```

```


Variable: **InferiorThread.details**

> 变量：InferiorThread.details


:   A string containing target specific thread state information. The format of this string varies by target. If there is no additional state information for this thread, then this attribute contains `None`.

> 一个包含特定目标线程状态信息的字符串。该字符串的格式因目标而异。如果此线程没有其他状态信息，则此属性包含“无”。

```
For example, on a [GNU]'](General-Query-Packets.html#qThreadExtraInfo)).

[GDB]'](Threads.html#info_005fthreads)).
```


A `gdb.InferiorThread` object has the following methods:

> 一个`gdb.InferiorThread`对象具有以下方法：


Function: **InferiorThread.is_valid** *()*

> 功能：**InferiorThread.is_valid**（）


:   Returns `True` if the `gdb.InferiorThread` object is valid, `False` if not. A `gdb.InferiorThread` object will become invalid if the thread exits, or the inferior that the thread belongs is deleted. All other `gdb.InferiorThread` methods will throw an exception if it is invalid at the time the method is called.

> 返回`True`如果`gdb.InferiorThread`对象有效，`False`如果无效。如果线程退出或属于该线程的次级被删除，`gdb.InferiorThread`对象将变得无效。如果在调用方法时无效，所有其他`gdb.InferiorThread`方法将抛出异常。

```

```


Function: **InferiorThread.switch** *()*

> 功能：**InferiorThread.switch** *（）*


:   This changes [GDB]'s currently selected thread to the one represented by this object.

> 这会更改GDB当前选定的线程为由此对象表示的线程。

```

```


Function: **InferiorThread.is_stopped** *()*

> 功能：**InferiorThread.is_stopped** *（）*


:   Return a Boolean indicating whether the thread is stopped.

> 返回一个布尔值，指示线程是否已停止。

```

```


Function: **InferiorThread.is_running** *()*

> 功能：InferiorThread.is_running（）


:   Return a Boolean indicating whether the thread is running.

> 返回一个布尔值，指示线程是否正在运行。

```

```


Function: **InferiorThread.is_exited** *()*

> 功能：**InferiorThread.is_exited** *（）*


:   Return a Boolean indicating whether the thread is exited.

> 返回一个布尔值，指示线程是否已退出。

```

```


Function: **InferiorThread.handle** *()*

> 功能：**InferiorThread.handle** *（）*


:   Return the thread object's handle, represented as a Python `bytes` object. A `gdb.Value` representation of the handle may be constructed via `gdb.Value(bufobj, type)` where `bufobj` is a `gdb.Type` for the handle type.

> 返回线程对象的句柄，表示为Python `bytes`对象。可以通过`gdb.Value(bufobj, type)`构造`gdb.Value`表示句柄，其中`bufobj`是句柄类型的`gdb.Type`。

---

::: header
Next: [Recordings In Python](Recordings-In-Python.html#Recordings-In-Python)]
:::
