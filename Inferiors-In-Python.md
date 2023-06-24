---
tip: translate by openai@2023-06-24 10:19:31
...
---
description: Inferiors In Python (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Inferiors In Python (Debugging with GDB)
lang: en
resource-type: document
title: Inferiors In Python (Debugging with GDB)
---
::: header
Next: [Events In Python](Events-In-Python.html#Events-In-Python)]
:::

---

#### 23.3.2.16 Inferiors In Python


Programs which are being run under [GDB] via objects of the `gdb.Inferior` class.

> 程序通过`gdb.Inferior`类的对象在GDB下运行。


The following inferior-related functions are available in the `gdb` module:

> `gdb` 模块中可用的以下与下属相关的功能：

Function: **gdb.inferiors** *()*

:   Return a tuple containing all inferior objects.

```
<!-- -->
```

Function: **gdb.selected_inferior** *()*

:   Return an object representing the current inferior.

A `gdb.Inferior` object has the following attributes:

Variable: **Inferior.num**

:   ID of inferior, as assigned by GDB.

Variable: **Inferior.connection**


:   The `gdb.TargetConnection` for this inferior (see [Connections In Python](Connections-In-Python.html#Connections-In-Python)), or `None` if this inferior has no connection.

> 这个次级（参见[Python中的连接](Connections-In-Python.html#Connections-In-Python)）的`gdb.TargetConnection`，如果这个次级没有连接，则为`None`。

```
<!-- -->
```

Variable: **Inferior.connection_num**


:   ID of inferior's connection as assigned by [GDB], or None if the inferior is not connected to a target. See [Inferiors Connections and Programs](Inferiors-Connections-and-Programs.html#Inferiors-Connections-and-Programs). This is equivalent to `gdb.Inferior.connection.num` in the case where `gdb.Inferior.connection` is not `None`.

> ID，由[GDB]分配给下级连接的ID，如果下级未连接到目标，则为None。请参阅[Inferiors Connections and Programs]（Inferiors-Connections-and-Programs.html#Inferiors-Connections-and-Programs）。如果`gdb.Inferior.connection`不是`None`，则等效于`gdb.Inferior.connection.num`。

```
<!-- -->
```

Variable: **Inferior.pid**


:   Process ID of the inferior, as assigned by the underlying operating system.

> 进程ID，由底层操作系统分配。

```
<!-- -->
```

Variable: **Inferior.was_attached**


:   Boolean signaling whether the inferior was created using 'attach', or started by [GDB] itself.

> 布尔值信号，用于表明下属是否使用“附加”创建，或由GDB本身启动。

```
<!-- -->
```

Variable: **Inferior.main_name**


:   A string holding the name of this inferior's "main" function, if it can be determined. If the name of main is not known, this is `None`.

> 一个字符串保存这个次级的“主”函数的名称，如果可以确定的话。如果主函数的名称未知，这是None。

```
<!-- -->
```

Variable: **Inferior.progspace**


:   The inferior's program space. See [Progspaces In Python](Progspaces-In-Python.html#Progspaces-In-Python).

> 程序空间的下层。参见[Python中的程序空间](Progspaces-In-Python.html#Progspaces-In-Python)。

```
<!-- -->
```

Variable: **Inferior.arguments**


:   The inferior's command line arguments, if known. This corresponds to the `set args` and `show args` commands. See [Arguments](Arguments.html#Arguments).

> 命令行参数（如果已知）。这对应于`set args`和`show args`命令。参见[参数](Arguments.html#Arguments)。

```
When accessed, the value is a string holding all the arguments. The contents are quoted as they would be when passed to the shell. If there are no arguments, the value is `None`.

Either a string or a sequence of strings can be assigned to this attribute. When a string is assigned, it is assumed to have any necessary quoting for the shell; when a sequence is assigned, the quoting is applied by [GDB].
```

A `gdb.Inferior` object has the following methods:

Function: **Inferior.is_valid** *()*


:   Returns `True` if the `gdb.Inferior` object is valid, `False` if not. A `gdb.Inferior` object will become invalid if the inferior no longer exists within [GDB]. All other `gdb.Inferior` methods will throw an exception if it is invalid at the time the method is called.

> 返回`True`如果`gdb.Inferior`对象是有效的，`False`如果不是。如果在[GDB]中不再存在次级对象，`gdb.Inferior`对象将变得无效。如果在调用方法时无效，其他所有`gdb.Inferior`方法将抛出异常。

```
<!-- -->
```

Function: **Inferior.threads** *()*


:   This method returns a tuple holding all the threads which are valid when it is called. If there are no valid threads, the method will return an empty tuple.

> 这个方法返回一个元组，包含调用时所有有效的线程。如果没有有效的线程，该方法将返回一个空元组。

```
<!-- -->
```

Function: **Inferior.architecture** *()*


:   Return the `gdb.Architecture` (see [Architectures In Python](Architectures-In-Python.html#Architectures-In-Python)) for this inferior. This represents the architecture of the inferior as a whole. Some platforms can have multiple architectures in a single address space, so this may not match the architecture of a particular frame (see [Frames In Python](Frames-In-Python.html#Frames-In-Python)).

> 返回此劣等物的`gdb.Architecture`（参见[Python中的架构](Architectures-In-Python.html#Architectures-In-Python)）。这代表了劣等物的整体架构。某些平台可以在单个地址空间中有多个架构，因此这可能与特定框架的架构不匹配（参见[Python中的框架](Frames-In-Python.html#Frames-In-Python)）。

Function: **Inferior.read_memory** *(address, length)*


:   Read `length`. Returns a buffer object, which behaves much like an array or a string. It can be modified and given to the `Inferior.write_memory` function. In Python 3, the return value is a `memoryview` object.

> 读取`length`。返回一个缓冲区对象，它的行为就像一个数组或字符串。它可以被修改并被传递到`Inferior.write_memory`函数。在Python 3中，返回值是一个`memoryview`对象。

)*

:   Write the contents of `buffer` to be written.

Function: **Inferior.search_memory** *(address, length, pattern)*


:   Search a region of the inferior memory starting at `address` parameter must be a Python object which supports the buffer protocol, i.e., a string, an array or the object returned from `gdb.read_memory`. Returns a Python `Long` containing the address where the pattern was found, or `None` if the pattern could not be found.

> 在`address`参数指定的低端内存区域中搜索，该参数必须是一个支持缓冲协议的Python对象，即字符串、数组或`gdb.read_memory`返回的对象。返回一个Python `Long`，其中包含找到模式的地址，如果找不到模式则返回`None`。

Function: **Inferior.thread_from_handle** *(handle)*


:   Return the thread object corresponding to `handle`, a thread library specific data structure such as `pthread_t` for pthreads library implementations.

> 返回与`handle`对应的线程对象，该线程对象是线程库特定的数据结构，比如pthreads库实现中的`pthread_t`。

```
The function `Inferior.thread_from_thread_handle` provides the same functionality, but use of `Inferior.thread_from_thread_handle` is deprecated.
```


The environment that will be passed to the inferior can be changed from Python by using the following methods. These methods only take effect when the inferior is started -- they will not affect an inferior that is already executing.

> 可以通过以下方法从Python中更改传递给次级的环境。这些方法仅在启动次级时才会生效——它们不会影响正在执行的次级。

Function: **Inferior.clear_env** *()*


:   Clear the current environment variables that will be passed to this inferior.

> 清除将被传递给此次下级的当前环境变量。

Function: **Inferior.set_env** *(name, value)*


:   Set the environment variable `name` to have the indicated value. Both parameters must be strings.

> 设置环境变量`name`为指定的值。两个参数都必须是字符串。

Function: **Inferior.unset_env** *(name)*

:   Unset the environment variable `name` must be a string.

---

::: header
Next: [Events In Python](Events-In-Python.html#Events-In-Python)]
:::
