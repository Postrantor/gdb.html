---
description: Progspaces In Python (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Progspaces In Python (Debugging with GDB)
lang: en
resource-type: document
title: Progspaces In Python (Debugging with GDB)
---
::: header
Next: [Objfiles In Python](Objfiles-In-Python.html#Objfiles-In-Python)]
:::

---

#### 23.3.2.24 Program Spaces In Python

A program space, or *progspace*, represents a symbolic view of an address space. It consists of all of the objfiles of the program. See [Objfiles In Python](Objfiles-In-Python.html#Objfiles-In-Python). See [program spaces](Inferiors-Connections-and-Programs.html#Inferiors-Connections-and-Programs), for more details about program spaces.

The following progspace-related functions are available in the `gdb` module:

Function: **gdb.current_progspace** *()*

:   This function returns the program space of the currently selected inferior. See [Inferiors Connections and Programs](Inferiors-Connections-and-Programs.html#Inferiors-Connections-and-Programs). This is identical to `gdb.selected_inferior().progspace` (see [Inferiors In Python](Inferiors-In-Python.html#Inferiors-In-Python)) and is included for historical compatibility.

Function: **gdb.progspaces** *()*

:   Return a sequence of all the progspaces currently known to [GDB].

Each progspace is represented by an instance of the `gdb.Progspace` class.

Variable: **Progspace.filename**

:   The file name of the progspace as a string.

```
<!-- -->
```

Variable: **Progspace.pretty_printers**

:   The `pretty_printers` attribute is a list of functions. It is used to look up pretty-printers. A `Value` is passed to each function in order; if the function returns `None`, then the search continues. Otherwise, the return value should be an object which is used to format the value. See [Pretty Printing API](Pretty-Printing-API.html#Pretty-Printing-API), for more information.

```
<!-- -->
```

Variable: **Progspace.type_printers**

:   The `type_printers` attribute is a list of type printer objects. See [Type Printing API](Type-Printing-API.html#Type-Printing-API), for more information.

```
<!-- -->
```

Variable: **Progspace.frame_filters**

:   The `frame_filters` attribute is a dictionary of frame filter objects. See [Frame Filter API](Frame-Filter-API.html#Frame-Filter-API), for more information.

A program space has the following methods:

Function: **Progspace.block_for_pc** *(pc)*

:   Return the innermost `gdb.Block` containing the given `pc` value specified, the function will return `None`.

Function: **Progspace.find_pc_line** *(pc)*

:   Return the `gdb.Symtab_and_line` object corresponding to the `pc` is passed as an argument, then the `symtab` and `line` attributes of the returned `gdb.Symtab_and_line` object will be `None` and 0 respectively.

Function: **Progspace.is_valid** *()*

:   Returns `True` if the `gdb.Progspace` object is valid, `False` if not. A `gdb.Progspace` object can become invalid if the program space file it refers to is not referenced by any inferior. All other `gdb.Progspace` methods will throw an exception if it is invalid at the time the method is called.

Function: **Progspace.objfiles** *()*

:   Return a sequence of all the objfiles referenced by this program space. See [Objfiles In Python](Objfiles-In-Python.html#Objfiles-In-Python).

Function: **Progspace.solib_name** *(address)*

:   Return the name of the shared library holding the given `address` as a string, or `None`.

One may add arbitrary attributes to `gdb.Progspace` objects in the usual Python way. This is useful if, for example, one needs to do some extra record keeping associated with the program space.

In this contrived example, we want to perform some processing when an objfile with a certain symbol is loaded, but we only want to do this once because it is expensive. To achieve this we record the results with the program space because we can't predict when the desired objfile will be loaded.

::: smallexample

```bash
(gdb) python
def clear_objfiles_handler(event):
    event.progspace.expensive_computation = None
def expensive(symbol):
    """A mock routine to perform an "expensive" computation on symbol."""
    print ("Computing the answer to the ultimate question ...")
    return 42
def new_objfile_handler(event):
    objfile = event.new_objfile
    progspace = objfile.progspace
    if not hasattr(progspace, 'expensive_computation') or \
            progspace.expensive_computation is None:
        # We use 'main' for the symbol to keep the example simple.
        # Note: There's no current way to constrain the lookup
        # to one objfile.
        symbol = gdb.lookup_global_symbol('main')
        if symbol is not None:
            progspace.expensive_computation = expensive(symbol)
gdb.events.clear_objfiles.connect(clear_objfiles_handler)
gdb.events.new_objfile.connect(new_objfile_handler)
end
(gdb) file /tmp/hello
Reading symbols from /tmp/hello...
Computing the answer to the ultimate question ...
(gdb) python print gdb.current_progspace().expensive_computation
42
(gdb) run
Starting program: /tmp/hello
Hello.
[Inferior 1 (process 4242) exited normally]
```

:::

---

::: header
Next: [Objfiles In Python](Objfiles-In-Python.html#Objfiles-In-Python)]
:::
