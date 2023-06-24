---
tip: translate by openai@2023-06-24 00:39:19
...
---
description: Objfiles In Python (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Objfiles In Python (Debugging with GDB)
lang: en
resource-type: document
title: Objfiles In Python (Debugging with GDB)
---
::: header
Next: [Frames In Python](Frames-In-Python.html#Frames-In-Python)]
:::

---

#### 23.3.2.25 Objfiles In Python

[GDB] calls these symbol-containing files *objfiles*.


The following objfile-related functions are available in the `gdb` module:

> 以下 objfile 相关的函数可以在 `gdb` 模块中使用：

Function: **gdb.current_objfile** *()*


:   When auto-loading a Python script (see [Python Auto-loading](Python-Auto_002dloading.html#Python-Auto_002dloading)), [GDB] sets the "current objfile" to the corresponding objfile. This function returns the current objfile. If there is no current objfile, this function returns `None`.

> 当自动加载Python脚本（参见[Python自动加载](Python-Auto_002dloading.html#Python-Auto_002dloading))时，[GDB]将“当前objfile”设置为相应的objfile。此函数返回当前objfile。如果没有当前objfile，则此函数返回`None`。

Function: **gdb.objfiles** *()*


:   Return a sequence of objfiles referenced by the current program space. See [Objfiles In Python](#Objfiles-In-Python), and [Progspaces In Python](Progspaces-In-Python.html#Progspaces-In-Python). This is identical to `gdb.selected_inferior().progspace.objfiles()` and is included for historical compatibility.

> 返回当前程序空间引用的一系列obj文件。请参见[Python中的Obj文件](#Objfiles-In-Python)和[Python中的Progspaces](Progspaces-In-Python.html#Progspaces-In-Python)。这与`gdb.selected_inferior().progspace.objfiles()`相同，仅出于历史兼容性考虑而包含。

)*


:   Look up `name`, a file name or build ID, in the list of objfiles for the current program space (see [Progspaces In Python](Progspaces-In-Python.html#Progspaces-In-Python)). If the objfile is not found throw the Python `ValueError` exception.

> 查找当前程序空间（参见[Python中的Progspaces]（Progspaces-In-Python.html#Progspaces-In-Python））中文件名或构建ID的`name`。如果找不到objfile，则抛出Python `ValueError`异常。

```
If `name`.

If `by_build_id` command-line option in [Command Line Options](http://sourceware.org/binutils/docs/ld/Options.html#Options) in The GNU Linker.
```

Each objfile is represented by an instance of the `gdb.Objfile` class.

Variable: **Objfile.filename**


:   The file name of the objfile as a string, with symbolic links resolved.

> 字符串中的obj文件名称，已解析符号链接。

```
The value is `None` if the objfile is no longer valid. See the `gdb.Objfile.is_valid` method, described below.
```

```
<!-- -->
```

Variable: **Objfile.username**

:   The file name of the objfile as specified by the user as a string.

```
The value is `None` if the objfile is no longer valid. See the `gdb.Objfile.is_valid` method, described below.
```

```
<!-- -->
```

Variable: **Objfile.is_file**


:   An objfile often comes from an ordinary file, but in some cases it may be constructed from the contents of memory. This attribute is `True` for file-backed objfiles, and `False` for other kinds.

> 一个objfile通常来自普通文件，但在某些情况下，它可以从内存中构造出来。这个属性对于文件驱动的objfile是`True`，对于其他类型则是`False`。

```
<!-- -->
```

Variable: **Objfile.owner**


:   For separate debug info objfiles this is the corresponding `gdb.Objfile` object that debug info is being provided for. Otherwise this is `None`. Separate debug info objfiles are added with the `gdb.Objfile.add_separate_debug_file` method, described below.

> 对于单独的调试信息obj文件，这是相应的`gdb.Objfile`对象，提供调试信息。否则为`None`。单独的调试信息obj文件可以使用下面描述的`gdb.Objfile.add_separate_debug_file`方法添加。

```
<!-- -->
```

Variable: **Objfile.build_id**


:   The build ID of the objfile as a string. If the objfile does not have a build ID then the value is `None`.

> 这个obj文件的构建ID作为一个字符串。如果obj文件没有构建ID，那么值为“无”。

```
This is supported only on some operating systems, notably those which use the ELF format for binary files and the [GNU] command-line option in [Command Line Options](http://sourceware.org/binutils/docs/ld/Options.html#Options) in The GNU Linker.
```

```
<!-- -->
```

Variable: **Objfile.progspace**


:   The containing program space of the objfile as a `gdb.Progspace` object. See [Progspaces In Python](Progspaces-In-Python.html#Progspaces-In-Python).

> 程序文件的包含空间作为一个`gdb.Progspace`对象。参见[Python中的Progspaces](Progspaces-In-Python.html#Progspaces-In-Python)。

```
<!-- -->
```

Variable: **Objfile.pretty_printers**


:   The `pretty_printers` attribute is a list of functions. It is used to look up pretty-printers. A `Value` is passed to each function in order; if the function returns `None`, then the search continues. Otherwise, the return value should be an object which is used to format the value. See [Pretty Printing API](Pretty-Printing-API.html#Pretty-Printing-API), for more information.

> `pretty_printers`属性是一个函数列表，用于查找美化打印器。将`Value`传递给每个函数，如果函数返回`None`，则搜索继续进行。否则，返回值应该是一个用于格式化值的对象。有关更多信息，请参阅[Pretty Printing API](Pretty-Printing-API.html#Pretty-Printing-API)。

```
<!-- -->
```

Variable: **Objfile.type_printers**


:   The `type_printers` attribute is a list of type printer objects. See [Type Printing API](Type-Printing-API.html#Type-Printing-API), for more information.

> `属性`type_printers`是一个类型打印机对象列表。更多信息请参阅[类型打印API](Type-Printing-API.html#Type-Printing-API)。

```
<!-- -->
```

Variable: **Objfile.frame_filters**


:   The `frame_filters` attribute is a dictionary of frame filter objects. See [Frame Filter API](Frame-Filter-API.html#Frame-Filter-API), for more information.

> `frame_filters`属性是一个字典，其中包含帧过滤器对象。有关更多信息，请参阅[帧过滤器API](Frame-Filter-API.html#Frame-Filter-API)。


One may add arbitrary attributes to `gdb.Objfile` objects in the usual Python way. This is useful if, for example, one needs to do some extra record keeping associated with the objfile.

> 可以以通常的Python方式给`gdb.Objfile`对象添加任意属性。如果需要做一些与objfile相关的额外记录，这将非常有用。


In this contrived example we record the time when [GDB] loaded the objfile.

> 在这个约定的例子中，我们记录[GDB]加载objfile的时间。

::: smallexample

```bash
(gdb) python
import datetime
def new_objfile_handler(event):
    # Set the time_loaded attribute of the new objfile.
    event.new_objfile.time_loaded = datetime.datetime.today()
gdb.events.new_objfile.connect(new_objfile_handler)
end
(gdb) file ./hello
Reading symbols from ./hello...
(gdb) python print gdb.objfiles()[0].time_loaded
2014-10-09 11:41:36.770345
```

:::

A `gdb.Objfile` object has the following methods:

Function: **Objfile.is_valid** *()*


:   Returns `True` if the `gdb.Objfile` object is valid, `False` if not. A `gdb.Objfile` object can become invalid if the object file it refers to is not loaded in [GDB] any longer. All other `gdb.Objfile` methods will throw an exception if it is invalid at the time the method is called.

> 如果`gdb.Objfile`对象有效，则返回`True`，如果无效，则返回`False`。如果它引用的对象文件不再在[GDB]中加载，则`gdb.Objfile`对象可能会变得无效。如果在调用方法时无效，则所有其他`gdb.Objfile`方法都会抛出异常。

```
<!-- -->
```

Function: **Objfile.add_separate_debug_file** *(file)*


:   Add `file` searches then this function can be used to add a debug info file from a different place.

> 添加`文件`搜索，然后可以使用此功能从不同的地方添加调试信息文件。

```
<!-- -->
```

)*


:   Search for a global symbol named `name` argument must be a domain constant defined in the `gdb` module and described in [Symbols In Python](Symbols-In-Python.html#Symbols-In-Python). This function is similar to `gdb.lookup_global_symbol`, except that the search is limited to this objfile.

> 搜索名为`name`参数的全局符号，该参数必须是`gdb`模块中定义的域常量，并在[Python中的符号](Symbols-In-Python.html#Symbols-In-Python)中有描述。此函数与`gdb.lookup_global_symbol`类似，但搜索范围仅限于此objfile。

```
The result is a `gdb.Symbol` object or `None` if the symbol is not found.
```

```
<!-- -->
```

)*


:   Like `Objfile.lookup_global_symbol`, but searches for a global symbol with static linkage named `name` in this objfile.

> 像`Objfile.lookup_global_symbol`一样，但搜索此objfile中具有静态链接的名为`name`的全局符号。

---

::: header
Next: [Frames In Python](Frames-In-Python.html#Frames-In-Python)]
:::
