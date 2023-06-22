---
description: Symbol Tables In Python (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Symbol Tables In Python (Debugging with GDB)
lang: en
resource-type: document
title: Symbol Tables In Python (Debugging with GDB)
---
::: header
Next: [Line Tables In Python](Line-Tables-In-Python.html#Line-Tables-In-Python)]
:::

---

#### 23.3.2.29 Symbol table representation in Python

Access to symbol table data maintained by [GDB] on the inferior is exposed to Python via two objects: `gdb.Symtab_and_line` and `gdb.Symtab`. Symbol table and line data for a frame is returned from the `find_sal` method in `gdb.Frame` object. See [Frames In Python](Frames-In-Python.html#Frames-In-Python).

For more information on [GDB]'s symbol table management, see [Examining the Symbol Table](Symbols.html#Symbols), for more information.

A `gdb.Symtab_and_line` object has the following attributes:

Variable: **Symtab_and_line.symtab**

:   The symbol table object (`gdb.Symtab`) for this frame. This attribute is not writable.

```
<!-- -->
```

Variable: **Symtab_and_line.pc**

:   Indicates the start of the address range occupied by code for the current source line. This attribute is not writable.

```
<!-- -->
```

Variable: **Symtab_and_line.last**

:   Indicates the end of the address range occupied by code for the current source line. This attribute is not writable.

```
<!-- -->
```

Variable: **Symtab_and_line.line**

:   Indicates the current line number for this object. This attribute is not writable.

A `gdb.Symtab_and_line` object has the following methods:

Function: **Symtab_and_line.is_valid** *()*

:   Returns `True` if the `gdb.Symtab_and_line` object is valid, `False` if not. A `gdb.Symtab_and_line` object can become invalid if the Symbol table and line object it refers to does not exist in [GDB] any longer. All other `gdb.Symtab_and_line` methods will throw an exception if it is invalid at the time the method is called.

A `gdb.Symtab` object has the following attributes:

Variable: **Symtab.filename**

:   The symbol table's source filename. This attribute is not writable.

```
<!-- -->
```

Variable: **Symtab.objfile**

:   The symbol table's backing object file. See [Objfiles In Python](Objfiles-In-Python.html#Objfiles-In-Python). This attribute is not writable.

```
<!-- -->
```

Variable: **Symtab.producer**

:   The name and possibly version number of the program that compiled the code in the symbol table. The contents of this string is up to the compiler. If no producer information is available then `None` is returned. This attribute is not writable.

A `gdb.Symtab` object has the following methods:

Function: **Symtab.is_valid** *()*

:   Returns `True` if the `gdb.Symtab` object is valid, `False` if not. A `gdb.Symtab` object can become invalid if the symbol table it refers to does not exist in [GDB] any longer. All other `gdb.Symtab` methods will throw an exception if it is invalid at the time the method is called.

```
<!-- -->
```

Function: **Symtab.fullname** *()*

:   Return the symbol table's source absolute file name.

```
<!-- -->
```

Function: **Symtab.global_block** *()*

:   Return the global block of the underlying symbol table. See [Blocks In Python](Blocks-In-Python.html#Blocks-In-Python).

```
<!-- -->
```

Function: **Symtab.static_block** *()*

:   Return the static block of the underlying symbol table. See [Blocks In Python](Blocks-In-Python.html#Blocks-In-Python).

```
<!-- -->
```

Function: **Symtab.linetable** *()*

:   Return the line table associated with the symbol table. See [Line Tables In Python](Line-Tables-In-Python.html#Line-Tables-In-Python).

---

::: header
Next: [Line Tables In Python](Line-Tables-In-Python.html#Line-Tables-In-Python)]
:::
