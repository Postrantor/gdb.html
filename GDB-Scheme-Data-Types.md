---
tip: translate by openai@2023-06-23 12:20:09
...
---
description: GDB Scheme Data Types (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: GDB Scheme Data Types (Debugging with GDB)
lang: en
resource-type: document
title: GDB Scheme Data Types (Debugging with GDB)
---
::: header
Next: [Guile Exception Handling](Guile-Exception-Handling.html#Guile-Exception-Handling)]
:::

---

#### 23.4.3.3 GDB Scheme Data Types


The values exposed by [GDB] object, and each is disjoint from all other types known to Guile.

> [GDB] 对象所暴露的值，每一个都与 Guile 所知的所有其他类型不相交。


Scheme Procedure: **gdb-object-kind** *object*

> 方案程序：**gdb-object-kind** *对象*


:   Return the kind of the [GDB] object, e.g., `<gdb:breakpoint>`, as a symbol.

> 返回[GDB]对象的类型，例如`<gdb:breakpoint>`，作为一个符号。


[GDB] defines the following object types:

> GDB 定义了以下对象类型：

`<gdb:arch>`


:   See [Architectures In Guile](Architectures-In-Guile.html#Architectures-In-Guile).

> 请看[Guile中的架构](Architectures-In-Guile.html#Architectures-In-Guile)。

`<gdb:block>`


:   See [Blocks In Guile](Blocks-In-Guile.html#Blocks-In-Guile).

> 请参阅[Guile中的块](Blocks-In-Guile.html#Blocks-In-Guile)。

`<gdb:block-symbols-iterator>`


:   See [Blocks In Guile](Blocks-In-Guile.html#Blocks-In-Guile).

> 请参阅[Guile中的块](Blocks-In-Guile.html#Blocks-In-Guile)。

`<gdb:breakpoint>`


:   See [Breakpoints In Guile](Breakpoints-In-Guile.html#Breakpoints-In-Guile).

> 请参阅[Guile中的断点](Breakpoints-In-Guile.html#Breakpoints-In-Guile)。

`<gdb:command>`


:   See [Commands In Guile](Commands-In-Guile.html#Commands-In-Guile).

> 请参阅[Guile中的命令](Commands-In-Guile.html#Commands-In-Guile)。

`<gdb:exception>`


:   See [Guile Exception Handling](Guile-Exception-Handling.html#Guile-Exception-Handling).

> 请参阅[Guile异常处理](Guile-Exception-Handling.html#Guile-Exception-Handling)。

`<gdb:frame>`


:   See [Frames In Guile](Frames-In-Guile.html#Frames-In-Guile).

> 请参见[Guile中的框架](Frames-In-Guile.html#Frames-In-Guile)。

`<gdb:iterator>`


:   See [Iterators In Guile](Iterators-In-Guile.html#Iterators-In-Guile).

> 请看[Guile中的迭代器](Iterators-In-Guile.html#Iterators-In-Guile)。

`<gdb:lazy-string>`


:   See [Lazy Strings In Guile](Lazy-Strings-In-Guile.html#Lazy-Strings-In-Guile).

> 请参阅[Guile中的懒惰字符串](Lazy-Strings-In-Guile.html#Lazy-Strings-In-Guile)。

`<gdb:objfile>`


:   See [Objfiles In Guile](Objfiles-In-Guile.html#Objfiles-In-Guile).

> 请参阅[Guile中的Objfiles](Objfiles-In-Guile.html#Objfiles-In-Guile)。

`<gdb:parameter>`


:   See [Parameters In Guile](Parameters-In-Guile.html#Parameters-In-Guile).

> 请参阅[Guile中的参数](Parameters-In-Guile.html#Parameters-In-Guile)。

`<gdb:pretty-printer>`


:   See [Guile Pretty Printing API](Guile-Pretty-Printing-API.html#Guile-Pretty-Printing-API).

> 请参阅[Guile Pretty Printing API](Guile-Pretty-Printing-API.html#Guile-Pretty-Printing-API)。

`<gdb:pretty-printer-worker>`


:   See [Guile Pretty Printing API](Guile-Pretty-Printing-API.html#Guile-Pretty-Printing-API).

> 请参阅[Guile Pretty Printing API](Guile-Pretty-Printing-API.html#Guile-Pretty-Printing-API)。

`<gdb:progspace>`


:   See [Progspaces In Guile](Progspaces-In-Guile.html#Progspaces-In-Guile).

> 请参阅[Guile中的Progspaces](Progspaces-In-Guile.html#Progspaces-In-Guile)。

`<gdb:symbol>`


:   See [Symbols In Guile](Symbols-In-Guile.html#Symbols-In-Guile).

> 请参阅[Guile中的符号](Symbols-In-Guile.html#Symbols-In-Guile)。

`<gdb:symtab>`


:   See [Symbol Tables In Guile](Symbol-Tables-In-Guile.html#Symbol-Tables-In-Guile).

> 请参见[Guile中的符号表](Symbol-Tables-In-Guile.html#Symbol-Tables-In-Guile)。

`<gdb:sal>`


:   See [Symbol Tables In Guile](Symbol-Tables-In-Guile.html#Symbol-Tables-In-Guile).

> 请参阅[Guile中的符号表](Symbol-Tables-In-Guile.html#Symbol-Tables-In-Guile)。

`<gdb:type>`


:   See [Types In Guile](Types-In-Guile.html#Types-In-Guile).

> 请参阅[Guile中的类型](Types-In-Guile.html#Types-In-Guile)。

`<gdb:field>`


:   See [Types In Guile](Types-In-Guile.html#Types-In-Guile).

> 请参阅[Guile中的类型](Types-In-Guile.html#Types-In-Guile)。

`<gdb:value>`


:   See [Values From Inferior In Guile](Values-From-Inferior-In-Guile.html#Values-From-Inferior-In-Guile).

> 请看[Guile中的下级值](Values-From-Inferior-In-Guile.html#Values-From-Inferior-In-Guile)。


The following [GDB] objects are managed internally so that the Scheme function `eq?` may be applied to them.

> 以下[GDB]对象由内部管理，以便可以将Scheme函数`eq？`应用于它们。

`<gdb:arch>`

`<gdb:block>`

`<gdb:breakpoint>`

`<gdb:frame>`

`<gdb:objfile>`

`<gdb:progspace>`

`<gdb:symbol>`

`<gdb:symtab>`

`<gdb:type>`

---

::: header
Next: [Guile Exception Handling](Guile-Exception-Handling.html#Guile-Exception-Handling)]
:::
