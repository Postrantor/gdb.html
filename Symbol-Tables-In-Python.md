---
tip: translate by openai@2023-06-24 03:28:31
...
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

> 访问[GDB]在次级维护的符号表数据可以通过两个对象：`gdb.Symtab_and_line`和`gdb.Symtab`来暴露给Python。框架的符号表和行数据可以从`gdb.Frame`对象的`find_sal`方法中返回，详见[Python中的框架](Frames-In-Python.html#Frames-In-Python)。


For more information on [GDB]'s symbol table management, see [Examining the Symbol Table](Symbols.html#Symbols), for more information.

> 若要了解更多关于GDB的符号表管理，请参阅[检查符号表](Symbols.html#Symbols)，以获取更多信息。

A `gdb.Symtab_and_line` object has the following attributes:

Variable: **Symtab_and_line.symtab**


:   The symbol table object (`gdb.Symtab`) for this frame. This attribute is not writable.

> 这个帧的符号表对象（`gdb.Symtab`）。此属性不可写。

```
<!-- -->
```

Variable: **Symtab_and_line.pc**


:   Indicates the start of the address range occupied by code for the current source line. This attribute is not writable.

> “：”表示当前源代码行所占用的地址范围的开始。此属性不可写。

```
<!-- -->
```

Variable: **Symtab_and_line.last**


:   Indicates the end of the address range occupied by code for the current source line. This attribute is not writable.

> : 表示当前源代码行占用的地址范围的结尾。此属性不可写。

```
<!-- -->
```

Variable: **Symtab_and_line.line**


:   Indicates the current line number for this object. This attribute is not writable.

> 这个属性表示当前对象的行号，不可写。

A `gdb.Symtab_and_line` object has the following methods:

Function: **Symtab_and_line.is_valid** *()*


:   Returns `True` if the `gdb.Symtab_and_line` object is valid, `False` if not. A `gdb.Symtab_and_line` object can become invalid if the Symbol table and line object it refers to does not exist in [GDB] any longer. All other `gdb.Symtab_and_line` methods will throw an exception if it is invalid at the time the method is called.

> 如果`gdb.Symtab_and_line`对象有效，则返回`True`，如果无效，则返回`False`。如果它所引用的符号表和行对象不再存在[GDB]中，则`gdb.Symtab_and_line`对象可能会失效。调用其他所有`gdb.Symtab_and_line`方法时，如果它处于无效状态，则会抛出异常。

A `gdb.Symtab` object has the following attributes:

Variable: **Symtab.filename**

:   The symbol table's source filename. This attribute is not writable.

```
<!-- -->
```

Variable: **Symtab.objfile**


:   The symbol table's backing object file. See [Objfiles In Python](Objfiles-In-Python.html#Objfiles-In-Python). This attribute is not writable.

> 这个符号表的后备对象文件。请参阅[Python中的对象文件](Objfiles-In-Python.html#Objfiles-In-Python)。这个属性是不可写的。

```
<!-- -->
```

Variable: **Symtab.producer**


:   The name and possibly version number of the program that compiled the code in the symbol table. The contents of this string is up to the compiler. If no producer information is available then `None` is returned. This attribute is not writable.

> 程序的名称和可能的版本号用于编译符号表中的代码。该字符串的内容取决于编译器。如果没有生产者信息可用，则返回“无”。此属性不可写。

A `gdb.Symtab` object has the following methods:

Function: **Symtab.is_valid** *()*


:   Returns `True` if the `gdb.Symtab` object is valid, `False` if not. A `gdb.Symtab` object can become invalid if the symbol table it refers to does not exist in [GDB] any longer. All other `gdb.Symtab` methods will throw an exception if it is invalid at the time the method is called.

> 如果`gdb.Symtab`对象有效，则返回`True`，如果无效，则返回`False`。如果在[GDB]中不再存在所引用的符号表，则`gdb.Symtab`对象可能会变得无效。如果在调用方法时无效，则所有其他`gdb.Symtab`方法都会引发异常。

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

> 返回底层符号表的全局块。参见[Python中的块](Blocks-In-Python.html#Blocks-In-Python)。

```
<!-- -->
```

Function: **Symtab.static_block** *()*


:   Return the static block of the underlying symbol table. See [Blocks In Python](Blocks-In-Python.html#Blocks-In-Python).

> 返回底层符号表的静态块。请参阅[Python中的块](Blocks-In-Python.html#Blocks-In-Python)。

```
<!-- -->
```

Function: **Symtab.linetable** *()*


:   Return the line table associated with the symbol table. See [Line Tables In Python](Line-Tables-In-Python.html#Line-Tables-In-Python).

> 返回与符号表相关联的行表。请参阅[Python中的行表](Line-Tables-In-Python.html#Line-Tables-In-Python)。

---

::: header
Next: [Line Tables In Python](Line-Tables-In-Python.html#Line-Tables-In-Python)]
:::
