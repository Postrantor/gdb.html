---
tip: translate by openai@2023-06-23 13:47:51
...
---
description: Symbol Tables In Python (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Symbol Tables In Python (Debugging with GDB)
lang: en
resource-type: document
title: Symbol Tables In Python (Debugging with GDB)
---------------------------------------------------

::: header
Next: [Line Tables In Python](Line-Tables-In-Python.html#Line-Tables-In-Python)]
:::

---

#### 23.3.2.29 Symbol table representation in Python

Access to symbol table data maintained by [GDB] on the inferior is exposed to Python via two objects: `gdb.Symtab_and_line` and `gdb.Symtab`. Symbol table and line data for a frame is returned from the `find_sal` method in `gdb.Frame` object. See [Frames In Python](Frames-In-Python.html#Frames-In-Python).

> 访问[GDB]在次级程序上维护的符号表数据可以通过两个对象：`gdb.Symtab_and_line` 和 `gdb.Symtab` 暴露给 Python。框架的符号表和行数据可以从 `gdb.Frame` 对象中的 `find_sal` 方法返回。参见 [Python 中的框架](Frames-In-Python.html#Frames-In-Python)。

For more information on [GDB]'s symbol table management, see [Examining the Symbol Table](Symbols.html#Symbols), for more information.

> 对于关于 GDB 的符号表管理的更多信息，请参阅检查符号表（Symbols.html#Symbols），以获取更多信息。

A `gdb.Symtab_and_line` object has the following attributes:

> 一个 `gdb.Symtab_and_line` 对象具有以下属性：

Variable: **Symtab_and_line.symtab**

> 变量：**Symtab_and_line.symtab**

:   The symbol table object (`gdb.Symtab`) for this frame. This attribute is not writable.

> 此框架的符号表对象（`gdb.Symtab`）。此属性不可写。

```

```

Variable: **Symtab_and_line.pc**

> 变量：**Symtab_and_line.pc**

:   Indicates the start of the address range occupied by code for the current source line. This attribute is not writable.

> : 表示当前源代码行所占用的地址范围的开始。此属性不可写。

```

```

Variable: **Symtab_and_line.last**

> 变量：**Symtab_and_line.last**

:   Indicates the end of the address range occupied by code for the current source line. This attribute is not writable.

> : 表示当前源代码行占用的地址范围的结尾。此属性不可写。

```

```

Variable: **Symtab_and_line.line**

> 变量：**Symtab_and_line.line**

:   Indicates the current line number for this object. This attribute is not writable.

> “:”表示此对象的当前行号。此属性不可写。

A `gdb.Symtab_and_line` object has the following methods:

> `gdb.Symtab_and_line` 对象具有以下方法：

Function: **Symtab_and_line.is_valid** *()*

> 功能：Symtab_and_line.is_valid（）

:   Returns `True` if the `gdb.Symtab_and_line` object is valid, `False` if not. A `gdb.Symtab_and_line` object can become invalid if the Symbol table and line object it refers to does not exist in [GDB] any longer. All other `gdb.Symtab_and_line` methods will throw an exception if it is invalid at the time the method is called.

> 返回 `True` 如果 `gdb.Symtab_and_line` 对象有效，`False` 如果没有。如果它引用的符号表和行对象不再存在[GDB]中，`gdb.Symtab_and_line` 对象可能会变得无效。调用其他 `gdb.Symtab_and_line` 方法时，如果它无效，则会抛出异常。

A `gdb.Symtab` object has the following attributes:

> 一个 `gdb.Symtab` 对象具有以下属性：

Variable: **Symtab.filename**

> 变量：**Symtab.filename**

:   The symbol table's source filename. This attribute is not writable.

> 符号表的源文件名。此属性不可写。

```

```

Variable: **Symtab.objfile**

> 变量：**Symtab.objfile**

:   The symbol table's backing object file. See [Objfiles In Python](Objfiles-In-Python.html#Objfiles-In-Python). This attribute is not writable.

> 这个符号表的后备对象文件。参见 [Python 中的 Objfiles](Objfiles-In-Python.html#Objfiles-In-Python)。这个属性不可写。

```

```

Variable: **Symtab.producer**

> 变量：**Symtab.producer**

:   The name and possibly version number of the program that compiled the code in the symbol table. The contents of this string is up to the compiler. If no producer information is available then `None` is returned. This attribute is not writable.

> 程式庫中的程式碼編譯所使用的程式名稱及版本號，該字串的內容取決於編譯器。如果沒有可用的產品資訊，則會傳回 'None'，該屬性不可寫入。

A `gdb.Symtab` object has the following methods:

> 一个 `gdb.Symtab` 对象具有以下方法：

Function: **Symtab.is_valid** *()*

> 功能：**Symtab.is_valid** *（）*

:   Returns `True` if the `gdb.Symtab` object is valid, `False` if not. A `gdb.Symtab` object can become invalid if the symbol table it refers to does not exist in [GDB] any longer. All other `gdb.Symtab` methods will throw an exception if it is invalid at the time the method is called.

> 如果 `gdb.Symtab` 对象有效，则返回 `True`，如果无效则返回 `False`。如果它所引用的符号表不再存在[GDB]中，那么 `gdb.Symtab` 对象可能会失效。调用其他 `gdb.Symtab` 方法时，如果它处于无效状态，则会抛出异常。

```

```

Function: **Symtab.fullname** *()*

> 功能：**Symtab.fullname** *（）*

:   Return the symbol table's source absolute file name.

> 返回符号表的源文件的绝对路径名。

```

```

Function: **Symtab.global_block** *()*

> 功能：**Symtab.global_block** *（）*

:   Return the global block of the underlying symbol table. See [Blocks In Python](Blocks-In-Python.html#Blocks-In-Python).

> 返回底层符号表的全局块。参见 [Python 中的块](Blocks-In-Python.html#Blocks-In-Python)。

```

```

Function: **Symtab.static_block** *()*

> 功能：**Symtab.static_block** *（）*

:   Return the static block of the underlying symbol table. See [Blocks In Python](Blocks-In-Python.html#Blocks-In-Python).

> 返回底层符号表的静态块。参见 [Python 中的块](Blocks-In-Python.html#Blocks-In-Python)。

```

```

Function: **Symtab.linetable** *()*

> 功能：**Symtab.linetable** *（）*

:   Return the line table associated with the symbol table. See [Line Tables In Python](Line-Tables-In-Python.html#Line-Tables-In-Python).

> 返回与符号表关联的行表。参见[Python 中的行表]（Line-Tables-In-Python.html#Line-Tables-In-Python）。

---

::: header
Next: [Line Tables In Python](Line-Tables-In-Python.html#Line-Tables-In-Python)]
:::
