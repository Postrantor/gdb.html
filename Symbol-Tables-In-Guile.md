---
tip: translate by openai@2023-06-24 03:27:16
...
---
description: Symbol Tables In Guile (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Symbol Tables In Guile (Debugging with GDB)
lang: en
resource-type: document
title: Symbol Tables In Guile (Debugging with GDB)
---
::: header
Next: [Breakpoints In Guile](Breakpoints-In-Guile.html#Breakpoints-In-Guile)]
:::

---

#### 23.4.3.18 Symbol table representation in Guile.


Access to symbol table data maintained by [GDB] on the inferior is exposed to Guile via two objects: `<gdb:sal>` (symtab-and-line) and `<gdb:symtab>`. Symbol table and line data for a frame is returned from the `frame-find-sal` `<gdb:frame>` procedure. See [Frames In Guile](Frames-In-Guile.html#Frames-In-Guile).

> 访问[GDB]在次级上维护的符号表数据通过两个对象对Guile暴露：`<gdb:sal>`（symtab-and-line）和`<gdb:symtab>`。帧的符号表和行数据由`frame-find-sal` `<gdb:frame>`过程返回。请参见[Guile中的帧](Frames-In-Guile.html#Frames-In-Guile)。


For more information on [GDB]'s symbol table management, see [Examining the Symbol Table](Symbols.html#Symbols).

> 要了解更多关于GDB的符号表管理的信息，请参阅检查符号表（Symbols.html#Symbols）。


The following symtab-related procedures are provided by the `(gdb)` module:

> 以下与symtab相关的程序由（gdb）模块提供：

Scheme Procedure: **symtab?** *object*


:   Return `#t` if `object` is an object of type `<gdb:symtab>`. Otherwise return `#f`.

> 如果`对象`是类型`<gdb:symtab>`的对象，则返回`#t`。否则返回`#f`。

```
<!-- -->
```

Scheme Procedure: **symtab-valid?** *symtab*


:   Return `#t` if the `<gdb:symtab>` object is valid, `#f` if not. A `<gdb:symtab>` object becomes invalid when the symbol table it refers to no longer exists in [GDB]. All other `<gdb:symtab>` procedures will throw an exception if it is invalid at the time the procedure is called.

> 如果<gdb:symtab>对象有效，则返回#t，如果无效，则返回#f。当它所引用的符号表不再存在于[GDB]中时，<gdb:symtab>对象将变得无效。其他所有<gdb:symtab>过程如果在调用时无效，则会抛出异常。

```
<!-- -->
```

Scheme Procedure: **symtab-filename** *symtab*

:   Return the symbol table's source filename.

```
<!-- -->
```

Scheme Procedure: **symtab-fullname** *symtab*

:   Return the symbol table's source absolute file name.

```
<!-- -->
```

Scheme Procedure: **symtab-objfile** *symtab*


:   Return the symbol table's backing object file. See [Objfiles In Guile](Objfiles-In-Guile.html#Objfiles-In-Guile).

> 返回符号表的支持对象文件。参见[Guile中的Objfiles](Objfiles-In-Guile.html#Objfiles-In-Guile)。

```
<!-- -->
```

Scheme Procedure: **symtab-global-block** *symtab*


:   Return the global block of the underlying symbol table. See [Blocks In Guile](Blocks-In-Guile.html#Blocks-In-Guile).

> 返回底层符号表的全局块。请参阅[Guile中的块](Blocks-In-Guile.html#Blocks-In-Guile)。

```
<!-- -->
```

Scheme Procedure: **symtab-static-block** *symtab*


:   Return the static block of the underlying symbol table. See [Blocks In Guile](Blocks-In-Guile.html#Blocks-In-Guile).

> 返回底层符号表的静态块。请参阅[Guile中的块](Blocks-In-Guile.html#Blocks-In-Guile)。


The following symtab-and-line-related procedures are provided by the `(gdb)` module:

> `(gdb)` 模块提供以下与符号表和行相关的程序：

Scheme Procedure: **sal?** *object*


:   Return `#t` if `object` is an object of type `<gdb:sal>`. Otherwise return `#f`.

> 如果对象是<gdb:sal>类型的对象，则返回#t。否则返回#f。

```
<!-- -->
```

Scheme Procedure: **sal-valid?** *sal*


:   Return `#t` if `sal`. All other `<gdb:sal>` procedures will throw an exception if it is invalid at the time the procedure is called.

> 如果sal有效，则返回#t，其他所有<gdb:sal>过程在调用时如果无效则抛出异常。

```
<!-- -->
```

Scheme Procedure: **sal-symtab** *sal*

:   Return the symbol table object (`<gdb:symtab>`) for `sal`.

```
<!-- -->
```

Scheme Procedure: **sal-line** *sal*

:   Return the line number for `sal`.

```
<!-- -->
```

Scheme Procedure: **sal-pc** *sal*

:   Return the start of the address range occupied by code for `sal`.

```
<!-- -->
```

Scheme Procedure: **sal-last** *sal*

:   Return the end of the address range occupied by code for `sal`.

```
<!-- -->
```

Scheme Procedure: **find-pc-line** *pc*


:   Return the `<gdb:sal>` object corresponding to the `pc` is passed as an argument, then the `symtab` and `line` attributes of the returned `<gdb:sal>` object will be `#f` and 0 respectively.

> 返回`<gdb:sal>`对象，该对象对应于作为参数传递的`pc`，然后返回的`<gdb:sal>`对象的`symtab`和`line`属性将分别为`#f`和0。

---

::: header
Next: [Breakpoints In Guile](Breakpoints-In-Guile.html#Breakpoints-In-Guile)]
:::
