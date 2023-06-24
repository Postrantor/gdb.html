---
tip: translate by openai@2023-06-24 01:31:37
...
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

> 一个程序空间，或者*progspace*，代表一个地址空间的象征视图。它由程序的所有objfiles组成。参见[Python中的Objfiles](Objfiles-In-Python.html#Objfiles-In-Python)。有关更多有关程序空间的详细信息，请参阅[程序空间](Inferiors-Connections-and-Programs.html#Inferiors-Connections-and-Programs)。


The following progspace-related functions are available in the `gdb` module:

> `gdb` 模块中提供以下与Progspace有关的功能：

Function: **gdb.current_progspace** *()*


:   This function returns the program space of the currently selected inferior. See [Inferiors Connections and Programs](Inferiors-Connections-and-Programs.html#Inferiors-Connections-and-Programs). This is identical to `gdb.selected_inferior().progspace` (see [Inferiors In Python](Inferiors-In-Python.html#Inferiors-In-Python)) and is included for historical compatibility.

> 这个函数返回当前选择的次级程序的程序空间。参见[次级连接和程序](Inferiors-Connections-and-Programs.html#Inferiors-Connections-and-Programs)。这与`gdb.selected_inferior().progspace`（参见[Python中的次级](Inferiors-In-Python.html#Inferiors-In-Python)）完全相同，仅为了历史兼容性而包含。

Function: **gdb.progspaces** *()*

:   Return a sequence of all the progspaces currently known to [GDB].


Each progspace is represented by an instance of the `gdb.Progspace` class.

> 每个progspace都由`gdb.Progspace`类的一个实例表示。

Variable: **Progspace.filename**

:   The file name of the progspace as a string.

```
<!-- -->
```

Variable: **Progspace.pretty_printers**


:   The `pretty_printers` attribute is a list of functions. It is used to look up pretty-printers. A `Value` is passed to each function in order; if the function returns `None`, then the search continues. Otherwise, the return value should be an object which is used to format the value. See [Pretty Printing API](Pretty-Printing-API.html#Pretty-Printing-API), for more information.

> `pretty_printers` 属性是一个函数列表，用于查找美化打印器。一个`Value`会传递给每个函数；如果函数返回`None`，则搜索继续。否则，返回值应该是一个用于格式化值的对象。有关更多信息，请参见[美化打印API](Pretty-Printing-API.html#Pretty-Printing-API)。

```
<!-- -->
```

Variable: **Progspace.type_printers**


:   The `type_printers` attribute is a list of type printer objects. See [Type Printing API](Type-Printing-API.html#Type-Printing-API), for more information.

> 属性`type_printers`是一个类型打印对象的列表。有关更多信息，请参阅[类型打印API](Type-Printing-API.html#Type-Printing-API)。

```
<!-- -->
```

Variable: **Progspace.frame_filters**


:   The `frame_filters` attribute is a dictionary of frame filter objects. See [Frame Filter API](Frame-Filter-API.html#Frame-Filter-API), for more information.

> `frame_filters`属性是一个帧过滤器对象的字典。有关更多信息，请参见[帧过滤器API](Frame-Filter-API.html#Frame-Filter-API)。

A program space has the following methods:

Function: **Progspace.block_for_pc** *(pc)*


:   Return the innermost `gdb.Block` containing the given `pc` value specified, the function will return `None`.

> 返回包含给定PC值的最内层gdb.Block，如果没有，函数将返回None。

Function: **Progspace.find_pc_line** *(pc)*


:   Return the `gdb.Symtab_and_line` object corresponding to the `pc` is passed as an argument, then the `symtab` and `line` attributes of the returned `gdb.Symtab_and_line` object will be `None` and 0 respectively.

> 返回`gdb.Symtab_and_line`对象对应传入的`pc`，那么返回的`gdb.Symtab_and_line`对象的`symtab`和`line`属性将分别为`None`和0。

Function: **Progspace.is_valid** *()*


:   Returns `True` if the `gdb.Progspace` object is valid, `False` if not. A `gdb.Progspace` object can become invalid if the program space file it refers to is not referenced by any inferior. All other `gdb.Progspace` methods will throw an exception if it is invalid at the time the method is called.

> 如果`gdb.Progspace`对象有效，则返回`True`，如果无效，则返回`False`。如果调用该方法时，它所引用的程序空间文件不被任何下级参考，`gdb.Progspace`对象将变得无效。其他所有`gdb.Progspace`方法都将抛出异常，如果它在调用方法时无效。

Function: **Progspace.objfiles** *()*


:   Return a sequence of all the objfiles referenced by this program space. See [Objfiles In Python](Objfiles-In-Python.html#Objfiles-In-Python).

> 返回此程序空间引用的所有objfile序列。请参阅[Python中的Objfiles](Objfiles-In-Python.html#Objfiles-In-Python)。

Function: **Progspace.solib_name** *(address)*


:   Return the name of the shared library holding the given `address` as a string, or `None`.

> 返回共享库的名称，其中包含给定的`地址`作为字符串，或`无`。


One may add arbitrary attributes to `gdb.Progspace` objects in the usual Python way. This is useful if, for example, one needs to do some extra record keeping associated with the program space.

> 一般的Python方式可以向`gdb.Progspace`对象添加任意属性。例如，如果需要与程序空间相关的额外记录，这将非常有用。


In this contrived example, we want to perform some processing when an objfile with a certain symbol is loaded, but we only want to do this once because it is expensive. To achieve this we record the results with the program space because we can't predict when the desired objfile will be loaded.

> 在这个精心构造的例子中，我们想要在加载具有某个特定符号的obj文件时执行一些处理，但我们只想这样做一次，因为这很昂贵。为了实现这一目标，我们将结果记录在程序空间中，因为我们无法预测何时加载所需的obj文件。

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
