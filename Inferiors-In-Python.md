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

The following inferior-related functions are available in the `gdb` module:

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

```
<!-- -->
```

Variable: **Inferior.connection_num**

:   ID of inferior's connection as assigned by [GDB], or None if the inferior is not connected to a target. See [Inferiors Connections and Programs](Inferiors-Connections-and-Programs.html#Inferiors-Connections-and-Programs). This is equivalent to `gdb.Inferior.connection.num` in the case where `gdb.Inferior.connection` is not `None`.

```
<!-- -->
```

Variable: **Inferior.pid**

:   Process ID of the inferior, as assigned by the underlying operating system.

```
<!-- -->
```

Variable: **Inferior.was_attached**

:   Boolean signaling whether the inferior was created using 'attach', or started by [GDB] itself.

```
<!-- -->
```

Variable: **Inferior.main_name**

:   A string holding the name of this inferior's "main" function, if it can be determined. If the name of main is not known, this is `None`.

```
<!-- -->
```

Variable: **Inferior.progspace**

:   The inferior's program space. See [Progspaces In Python](Progspaces-In-Python.html#Progspaces-In-Python).

```
<!-- -->
```

Variable: **Inferior.arguments**

:   The inferior's command line arguments, if known. This corresponds to the `set args` and `show args` commands. See [Arguments](Arguments.html#Arguments).

```
When accessed, the value is a string holding all the arguments. The contents are quoted as they would be when passed to the shell. If there are no arguments, the value is `None`.

Either a string or a sequence of strings can be assigned to this attribute. When a string is assigned, it is assumed to have any necessary quoting for the shell; when a sequence is assigned, the quoting is applied by [GDB].
```

A `gdb.Inferior` object has the following methods:

Function: **Inferior.is_valid** *()*

:   Returns `True` if the `gdb.Inferior` object is valid, `False` if not. A `gdb.Inferior` object will become invalid if the inferior no longer exists within [GDB]. All other `gdb.Inferior` methods will throw an exception if it is invalid at the time the method is called.

```
<!-- -->
```

Function: **Inferior.threads** *()*

:   This method returns a tuple holding all the threads which are valid when it is called. If there are no valid threads, the method will return an empty tuple.

```
<!-- -->
```

Function: **Inferior.architecture** *()*

:   Return the `gdb.Architecture` (see [Architectures In Python](Architectures-In-Python.html#Architectures-In-Python)) for this inferior. This represents the architecture of the inferior as a whole. Some platforms can have multiple architectures in a single address space, so this may not match the architecture of a particular frame (see [Frames In Python](Frames-In-Python.html#Frames-In-Python)).

Function: **Inferior.read_memory** *(address, length)*

:   Read `length`. Returns a buffer object, which behaves much like an array or a string. It can be modified and given to the `Inferior.write_memory` function. In Python 3, the return value is a `memoryview` object.

)*

:   Write the contents of `buffer` to be written.

Function: **Inferior.search_memory** *(address, length, pattern)*

:   Search a region of the inferior memory starting at `address` parameter must be a Python object which supports the buffer protocol, i.e., a string, an array or the object returned from `gdb.read_memory`. Returns a Python `Long` containing the address where the pattern was found, or `None` if the pattern could not be found.

Function: **Inferior.thread_from_handle** *(handle)*

:   Return the thread object corresponding to `handle`, a thread library specific data structure such as `pthread_t` for pthreads library implementations.

```
The function `Inferior.thread_from_thread_handle` provides the same functionality, but use of `Inferior.thread_from_thread_handle` is deprecated.
```

The environment that will be passed to the inferior can be changed from Python by using the following methods. These methods only take effect when the inferior is started -- they will not affect an inferior that is already executing.

Function: **Inferior.clear_env** *()*

:   Clear the current environment variables that will be passed to this inferior.

Function: **Inferior.set_env** *(name, value)*

:   Set the environment variable `name` to have the indicated value. Both parameters must be strings.

Function: **Inferior.unset_env** *(name)*

:   Unset the environment variable `name` must be a string.

---

::: header
Next: [Events In Python](Events-In-Python.html#Events-In-Python)]
:::