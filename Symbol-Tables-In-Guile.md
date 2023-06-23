---
tip: translate by openai@2023-06-23 13:45:23
...
---
description: Symbol Tables In Guile (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Symbol Tables In Guile (Debugging with GDB)
lang: en
resource-type: document
title: Symbol Tables In Guile (Debugging with GDB)
--------------------------------------------------

::: header
Next: [Breakpoints In Guile](Breakpoints-In-Guile.html#Breakpoints-In-Guile)]
:::

---

#### 23.4.3.18 Symbol table representation in Guile.

Access to symbol table data maintained by [GDB] on the inferior is exposed to Guile via two objects: `<gdb:sal>` (symtab-and-line) and `<gdb:symtab>`. Symbol table and line data for a frame is returned from the `frame-find-sal` `<gdb:frame>` procedure. See [Frames In Guile](Frames-In-Guile.html#Frames-In-Guile).

> 访问由[GDB]在次级上维护的符号表数据可以通过两个对象暴露给 Guile：`<gdb:sal>`（symtab-and-line）和 `<gdb:symtab>`。框架的符号表和行数据可以从 `frame-find-sal` `<gdb:frame>` 过程中返回。请参阅 [Guile 中的框架](Frames-In-Guile.html#Frames-In-Guile)。

For more information on [GDB]'s symbol table management, see [Examining the Symbol Table](Symbols.html#Symbols).

> 对于 GDB 的符号表管理的更多信息，请参见检查符号表（Symbols.html#Symbols）。

The following symtab-related procedures are provided by the `(gdb)` module:

> 以下 symtab 相关的程序由 `(gdb)` 模块提供：

Scheme Procedure: **symtab?** *object*

> 方案程序：**symtab?** *对象*

:   Return `#t` if `object` is an object of type `<gdb:symtab>`. Otherwise return `#f`.

> 如果对象是 [gdb:symtab](gdb:symtab) 类型的对象，则返回#t，否则返回#f。

```

```

Scheme Procedure: **symtab-valid?** *symtab*

> 模式过程：**symtab-valid？** *symtab*

:   Return `#t` if the `<gdb:symtab>` object is valid, `#f` if not. A `<gdb:symtab>` object becomes invalid when the symbol table it refers to no longer exists in [GDB]. All other `<gdb:symtab>` procedures will throw an exception if it is invalid at the time the procedure is called.

> 如果 [gdb:symtab](gdb:symtab) 对象有效，则返回#t，如果无效，则返回#f。当它引用的符号表不再存在于[GDB]中时，[gdb:symtab](gdb:symtab) 对象将变得无效。调用其他 [gdb:symtab](gdb:symtab) 过程时，如果它在调用时无效，则会抛出异常。

```

```

Scheme Procedure: **symtab-filename** *symtab*

> 程序：symtab-filename，参数：symtab

:   Return the symbol table's source filename.

> 返回符号表的源文件名。

```

```

Scheme Procedure: **symtab-fullname** *symtab*

> 程序：symtab-fullname，参数：symtab

:   Return the symbol table's source absolute file name.

> 返回符号表的源文件的绝对路径名。

```

```

Scheme Procedure: **symtab-objfile** *symtab*

> 程序设计：**symtab-objfile** *symtab*

:   Return the symbol table's backing object file. See [Objfiles In Guile](Objfiles-In-Guile.html#Objfiles-In-Guile).

> 返回符号表的支持对象文件。参见 [Guile 中的 Objfiles](Objfiles-In-Guile.html#Objfiles-In-Guile)。

```

```

Scheme Procedure: **symtab-global-block** *symtab*

> 程序设计方案：**symtab-global-block** *symtab*

:   Return the global block of the underlying symbol table. See [Blocks In Guile](Blocks-In-Guile.html#Blocks-In-Guile).

> 返回基础符号表的全局块。参见 [Guile 中的块](Blocks-In-Guile.html#Blocks-In-Guile)。

```

```

Scheme Procedure: **symtab-static-block** *symtab*

> 程序设计：**symtab-static-block** *symtab*

:   Return the static block of the underlying symbol table. See [Blocks In Guile](Blocks-In-Guile.html#Blocks-In-Guile).

> 返回底层符号表的静态块。参见 [Guile 中的块](Blocks-In-Guile.html#Blocks-In-Guile)。

The following symtab-and-line-related procedures are provided by the `(gdb)` module:

> `(gdb)` 模块提供以下与 symtab 和行相关的程序：

Scheme Procedure: **sal?** *object*

> 方案程序：**sal？** *对象*

:   Return `#t` if `object` is an object of type `<gdb:sal>`. Otherwise return `#f`.

> 如果 `对象` 是 `<gdb:sal>` 类型的对象，则返回 `#t`。否则返回 `#f`。

```

```

Scheme Procedure: **sal-valid?** *sal*

> 方案程序：**sal-valid？** *sal*

:   Return `#t` if `sal`. All other `<gdb:sal>` procedures will throw an exception if it is invalid at the time the procedure is called.

> 如果 `sal`，则返回 `#t`。如果调用该程序时无效，则所有其他 `<gdb:sal>` 程序都会抛出异常。

```

```

Scheme Procedure: **sal-symtab** *sal*

> 方案程序：**sal-symtab** *sal*

:   Return the symbol table object (`<gdb:symtab>`) for `sal`.

> 返回符号表对象（[gdb:symtab](gdb:symtab)）为 sal。

```

```

Scheme Procedure: **sal-line** *sal*

> 方案程序：**sal-line** *sal*

:   Return the line number for `sal`.

> 找到'sal'所在的行号

```

```

Scheme Procedure: **sal-pc** *sal*

> 方案程序：**sal-pc** *sal*

:   Return the start of the address range occupied by code for `sal`.

> 返回用于 `sal` 代码所占用的地址范围的起点。

```

```

Scheme Procedure: **sal-last** *sal*

> 方案步骤：**sal-last** *sal*

:   Return the end of the address range occupied by code for `sal`.

> 返回代码 `sal` 占用的地址范围的末尾。

```

```

Scheme Procedure: **find-pc-line** *pc*

> 找到 PC 线：**find-pc-line** *pc*

:   Return the `<gdb:sal>` object corresponding to the `pc` is passed as an argument, then the `symtab` and `line` attributes of the returned `<gdb:sal>` object will be `#f` and 0 respectively.

> 返回与作为参数传递的 `pc` 相对应的 `<gdb:sal>` 对象，然后返回的 `<gdb:sal>` 对象的 `symtab` 和 `line` 属性将分别为 `#f` 和 0。

---

::: header
Next: [Breakpoints In Guile](Breakpoints-In-Guile.html#Breakpoints-In-Guile)]
:::
