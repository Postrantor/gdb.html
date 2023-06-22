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

For more information on [GDB]'s symbol table management, see [Examining the Symbol Table](Symbols.html#Symbols).

The following symtab-related procedures are provided by the `(gdb)` module:

Scheme Procedure: **symtab?** *object*

:   Return `#t` if `object` is an object of type `<gdb:symtab>`. Otherwise return `#f`.

```
<!-- -->
```

Scheme Procedure: **symtab-valid?** *symtab*

:   Return `#t` if the `<gdb:symtab>` object is valid, `#f` if not. A `<gdb:symtab>` object becomes invalid when the symbol table it refers to no longer exists in [GDB]. All other `<gdb:symtab>` procedures will throw an exception if it is invalid at the time the procedure is called.

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

```
<!-- -->
```

Scheme Procedure: **symtab-global-block** *symtab*

:   Return the global block of the underlying symbol table. See [Blocks In Guile](Blocks-In-Guile.html#Blocks-In-Guile).

```
<!-- -->
```

Scheme Procedure: **symtab-static-block** *symtab*

:   Return the static block of the underlying symbol table. See [Blocks In Guile](Blocks-In-Guile.html#Blocks-In-Guile).

The following symtab-and-line-related procedures are provided by the `(gdb)` module:

Scheme Procedure: **sal?** *object*

:   Return `#t` if `object` is an object of type `<gdb:sal>`. Otherwise return `#f`.

```
<!-- -->
```

Scheme Procedure: **sal-valid?** *sal*

:   Return `#t` if `sal`. All other `<gdb:sal>` procedures will throw an exception if it is invalid at the time the procedure is called.

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

---

::: header
Next: [Breakpoints In Guile](Breakpoints-In-Guile.html#Breakpoints-In-Guile)]
:::
