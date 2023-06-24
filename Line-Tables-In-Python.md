---
tip: translate by openai@2023-06-23 23:51:26
...
---
description: Line Tables In Python (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Line Tables In Python (Debugging with GDB)
lang: en
resource-type: document
title: Line Tables In Python (Debugging with GDB)
---
::: header
Next: [Breakpoints In Python](Breakpoints-In-Python.html#Breakpoints-In-Python)]
:::

---

#### 23.3.2.30 Manipulating line tables using Python


Python code can request and inspect line table information from a symbol table that is loaded in [GDB]. A line table is a mapping of source lines to their executable locations in memory. To acquire the line table information for a particular symbol table, use the `linetable` function (see [Symbol Tables In Python](Symbol-Tables-In-Python.html#Symbol-Tables-In-Python)).

> Python 代码可以从加载在GDB中的符号表中请求和检查行表信息。行表是源行到其内存中可执行位置的映射。要获取特定符号表的行表信息，请使用`linetable`函数（请参阅[Python中的符号表](Symbol-Tables-In-Python.html#Symbol-Tables-In-Python))。


A `gdb.LineTable` is iterable. The iterator returns `LineTableEntry` objects that correspond to the source line and address for each line table entry. `LineTableEntry` objects have the following attributes:

> `gdb.LineTable`是可迭代的。迭代器返回与每个行表条目相对应的`LineTableEntry`对象。 `LineTableEntry`对象具有以下属性：

Variable: **LineTableEntry.line**


:   The source line number for this line table entry. This number corresponds to the actual line of source. This attribute is not writable.

> 此行表项的源代码行号。此数字对应于实际源代码的行。此属性不可写。

```
<!-- -->
```

Variable: **LineTableEntry.pc**


:   The address that is associated with the line table entry where the executable code for that source line resides in memory. This attribute is not writable.

> 所关联的行表条目中存放源代码的可执行代码的地址。此属性不可写。


As there can be multiple addresses for a single source line, you may receive multiple `LineTableEntry` objects with matching `line` attributes, but with different `pc` attributes. The iterator is sorted in ascending `pc` order. Here is a small example illustrating iterating over a line table.

> 由于一个源代码行可以有多个地址，您可能会收到多个具有匹配`line`属性但具有不同`pc`属性的`LineTableEntry`对象。迭代器按升序排列`pc`。以下是一个示例，演示如何遍历一个行表。

::: smallexample

```bash
symtab = gdb.selected_frame().find_sal().symtab
linetable = symtab.linetable()
for line in linetable:
   print ("Line: "+str(line.line)+" Address: "+hex(line.pc))
```

:::

This will have the following output:

::: smallexample

```bash
Line: 33 Address: 0x4005c8L
Line: 37 Address: 0x4005caL
Line: 39 Address: 0x4005d2L
Line: 40 Address: 0x4005f8L
Line: 42 Address: 0x4005ffL
Line: 44 Address: 0x400608L
Line: 42 Address: 0x40060cL
Line: 45 Address: 0x400615L
```

:::


In addition to being able to iterate over a `LineTable`, it also has the following direct access methods:

> 此外，除了可以遍历LineTable之外，它还具有以下直接访问方法：

Function: **LineTable.line** *(line)*


:   Return a Python `Tuple` of `LineTableEntry` objects for any entries in the line table for the given `line`, the Python `None` is returned.

> 返回一个Python元组，其中包含给定行的行表中的任何条目的`LineTableEntry`对象，如果没有，则返回Python的`None`。

```
<!-- -->
```

Function: **LineTable.has_line** *(line)*


:   Return a Python `Boolean` indicating whether there is an entry in the line table for this source line. Return `True` if an entry is found, or `False` if not.

> 返回一个Python布尔值，指示此源行是否在行表中有条目。如果找到条目，则返回“True”，如果没有，则返回“False”。

```
<!-- -->
```

Function: **LineTable.source_lines** *()*


:   Return a Python `List` of the source line numbers in the symbol table. Only lines with executable code locations are returned. The contents of the `List` will just be the source line entries represented as Python `Long` values.

> 返回一个Python列表，其中包含符号表中的源代码行号。只返回具有可执行代码位置的行。列表的内容只是以Python长值表示的源代码行条目。

---

::: header
Next: [Breakpoints In Python](Breakpoints-In-Python.html#Breakpoints-In-Python)]
:::
