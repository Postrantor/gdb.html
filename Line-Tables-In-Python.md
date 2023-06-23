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

A `gdb.LineTable` is iterable. The iterator returns `LineTableEntry` objects that correspond to the source line and address for each line table entry. `LineTableEntry` objects have the following attributes:

Variable: **LineTableEntry.line**

:   The source line number for this line table entry. This number corresponds to the actual line of source. This attribute is not writable.

```
<!-- -->
```

Variable: **LineTableEntry.pc**

:   The address that is associated with the line table entry where the executable code for that source line resides in memory. This attribute is not writable.

As there can be multiple addresses for a single source line, you may receive multiple `LineTableEntry` objects with matching `line` attributes, but with different `pc` attributes. The iterator is sorted in ascending `pc` order. Here is a small example illustrating iterating over a line table.

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

Function: **LineTable.line** *(line)*

:   Return a Python `Tuple` of `LineTableEntry` objects for any entries in the line table for the given `line`, the Python `None` is returned.

```
<!-- -->
```

Function: **LineTable.has_line** *(line)*

:   Return a Python `Boolean` indicating whether there is an entry in the line table for this source line. Return `True` if an entry is found, or `False` if not.

```
<!-- -->
```

Function: **LineTable.source_lines** *()*

:   Return a Python `List` of the source line numbers in the symbol table. Only lines with executable code locations are returned. The contents of the `List` will just be the source line entries represented as Python `Long` values.

---

::: header
Next: [Breakpoints In Python](Breakpoints-In-Python.html#Breakpoints-In-Python)]
:::
