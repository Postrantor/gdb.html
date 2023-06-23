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

Function: **gdb.current_objfile** *()*

:   When auto-loading a Python script (see [Python Auto-loading](Python-Auto_002dloading.html#Python-Auto_002dloading)), [GDB] sets the "current objfile" to the corresponding objfile. This function returns the current objfile. If there is no current objfile, this function returns `None`.

Function: **gdb.objfiles** *()*

:   Return a sequence of objfiles referenced by the current program space. See [Objfiles In Python](#Objfiles-In-Python), and [Progspaces In Python](Progspaces-In-Python.html#Progspaces-In-Python). This is identical to `gdb.selected_inferior().progspace.objfiles()` and is included for historical compatibility.

)*

:   Look up `name`, a file name or build ID, in the list of objfiles for the current program space (see [Progspaces In Python](Progspaces-In-Python.html#Progspaces-In-Python)). If the objfile is not found throw the Python `ValueError` exception.

```
If `name`.

If `by_build_id` command-line option in [Command Line Options](http://sourceware.org/binutils/docs/ld/Options.html#Options) in The GNU Linker.
```

Each objfile is represented by an instance of the `gdb.Objfile` class.

Variable: **Objfile.filename**

:   The file name of the objfile as a string, with symbolic links resolved.

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

```
<!-- -->
```

Variable: **Objfile.owner**

:   For separate debug info objfiles this is the corresponding `gdb.Objfile` object that debug info is being provided for. Otherwise this is `None`. Separate debug info objfiles are added with the `gdb.Objfile.add_separate_debug_file` method, described below.

```
<!-- -->
```

Variable: **Objfile.build_id**

:   The build ID of the objfile as a string. If the objfile does not have a build ID then the value is `None`.

```
This is supported only on some operating systems, notably those which use the ELF format for binary files and the [GNU] command-line option in [Command Line Options](http://sourceware.org/binutils/docs/ld/Options.html#Options) in The GNU Linker.
```

```
<!-- -->
```

Variable: **Objfile.progspace**

:   The containing program space of the objfile as a `gdb.Progspace` object. See [Progspaces In Python](Progspaces-In-Python.html#Progspaces-In-Python).

```
<!-- -->
```

Variable: **Objfile.pretty_printers**

:   The `pretty_printers` attribute is a list of functions. It is used to look up pretty-printers. A `Value` is passed to each function in order; if the function returns `None`, then the search continues. Otherwise, the return value should be an object which is used to format the value. See [Pretty Printing API](Pretty-Printing-API.html#Pretty-Printing-API), for more information.

```
<!-- -->
```

Variable: **Objfile.type_printers**

:   The `type_printers` attribute is a list of type printer objects. See [Type Printing API](Type-Printing-API.html#Type-Printing-API), for more information.

```
<!-- -->
```

Variable: **Objfile.frame_filters**

:   The `frame_filters` attribute is a dictionary of frame filter objects. See [Frame Filter API](Frame-Filter-API.html#Frame-Filter-API), for more information.

One may add arbitrary attributes to `gdb.Objfile` objects in the usual Python way. This is useful if, for example, one needs to do some extra record keeping associated with the objfile.

In this contrived example we record the time when [GDB] loaded the objfile.

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

```
<!-- -->
```

Function: **Objfile.add_separate_debug_file** *(file)*

:   Add `file` searches then this function can be used to add a debug info file from a different place.

```
<!-- -->
```

)*

:   Search for a global symbol named `name` argument must be a domain constant defined in the `gdb` module and described in [Symbols In Python](Symbols-In-Python.html#Symbols-In-Python). This function is similar to `gdb.lookup_global_symbol`, except that the search is limited to this objfile.

```
The result is a `gdb.Symbol` object or `None` if the symbol is not found.
```

```
<!-- -->
```

)*

:   Like `Objfile.lookup_global_symbol`, but searches for a global symbol with static linkage named `name` in this objfile.

---

::: header
Next: [Frames In Python](Frames-In-Python.html#Frames-In-Python)]
:::
