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

Scheme Procedure: **gdb-object-kind** *object*

:   Return the kind of the [GDB] object, e.g., `<gdb:breakpoint>`, as a symbol.

[GDB] defines the following object types:

`<gdb:arch>`

:   See [Architectures In Guile](Architectures-In-Guile.html#Architectures-In-Guile).

`<gdb:block>`

:   See [Blocks In Guile](Blocks-In-Guile.html#Blocks-In-Guile).

`<gdb:block-symbols-iterator>`

:   See [Blocks In Guile](Blocks-In-Guile.html#Blocks-In-Guile).

`<gdb:breakpoint>`

:   See [Breakpoints In Guile](Breakpoints-In-Guile.html#Breakpoints-In-Guile).

`<gdb:command>`

:   See [Commands In Guile](Commands-In-Guile.html#Commands-In-Guile).

`<gdb:exception>`

:   See [Guile Exception Handling](Guile-Exception-Handling.html#Guile-Exception-Handling).

`<gdb:frame>`

:   See [Frames In Guile](Frames-In-Guile.html#Frames-In-Guile).

`<gdb:iterator>`

:   See [Iterators In Guile](Iterators-In-Guile.html#Iterators-In-Guile).

`<gdb:lazy-string>`

:   See [Lazy Strings In Guile](Lazy-Strings-In-Guile.html#Lazy-Strings-In-Guile).

`<gdb:objfile>`

:   See [Objfiles In Guile](Objfiles-In-Guile.html#Objfiles-In-Guile).

`<gdb:parameter>`

:   See [Parameters In Guile](Parameters-In-Guile.html#Parameters-In-Guile).

`<gdb:pretty-printer>`

:   See [Guile Pretty Printing API](Guile-Pretty-Printing-API.html#Guile-Pretty-Printing-API).

`<gdb:pretty-printer-worker>`

:   See [Guile Pretty Printing API](Guile-Pretty-Printing-API.html#Guile-Pretty-Printing-API).

`<gdb:progspace>`

:   See [Progspaces In Guile](Progspaces-In-Guile.html#Progspaces-In-Guile).

`<gdb:symbol>`

:   See [Symbols In Guile](Symbols-In-Guile.html#Symbols-In-Guile).

`<gdb:symtab>`

:   See [Symbol Tables In Guile](Symbol-Tables-In-Guile.html#Symbol-Tables-In-Guile).

`<gdb:sal>`

:   See [Symbol Tables In Guile](Symbol-Tables-In-Guile.html#Symbol-Tables-In-Guile).

`<gdb:type>`

:   See [Types In Guile](Types-In-Guile.html#Types-In-Guile).

`<gdb:field>`

:   See [Types In Guile](Types-In-Guile.html#Types-In-Guile).

`<gdb:value>`

:   See [Values From Inferior In Guile](Values-From-Inferior-In-Guile.html#Values-From-Inferior-In-Guile).

The following [GDB] objects are managed internally so that the Scheme function `eq?` may be applied to them.

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
