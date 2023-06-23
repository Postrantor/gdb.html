---
description: Progspaces In Guile (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Progspaces In Guile (Debugging with GDB)
lang: en
resource-type: document
title: Progspaces In Guile (Debugging with GDB)
---
::: header
Next: [Objfiles In Guile](Objfiles-In-Guile.html#Objfiles-In-Guile)]
:::

---

#### 23.4.3.13 Program Spaces In Guile

A program space, or *progspace*, represents a symbolic view of an address space. It consists of all of the objfiles of the program. See [Objfiles In Guile](Objfiles-In-Guile.html#Objfiles-In-Guile). See [program spaces](Inferiors-Connections-and-Programs.html#Inferiors-Connections-and-Programs), for more details about program spaces.

Each progspace is represented by an instance of the `<gdb:progspace>` smob. See [GDB Scheme Data Types](GDB-Scheme-Data-Types.html#GDB-Scheme-Data-Types).

The following progspace-related functions are available in the `(gdb)` module:

Scheme Procedure: **progspace?** *object*

:   Return `#t` if `object` is a `<gdb:progspace>` object. Otherwise return `#f`.

```
<!-- -->
```

Scheme Procedure: **progspace-valid?** *progspace*

:   Return `#t` if `progspace` any longer.

```
<!-- -->
```

Scheme Procedure: **current-progspace**

:   This function returns the program space of the currently selected inferior. There is always a current progspace, this never returns `#f`. See [Inferiors Connections and Programs](Inferiors-Connections-and-Programs.html#Inferiors-Connections-and-Programs).

```
<!-- -->
```

Scheme Procedure: **progspaces**

:   Return a list of all the progspaces currently known to [GDB].

```
<!-- -->
```

Scheme Procedure: **progspace-filename** *progspace*

:   Return the absolute file name of `progspace` is started without a program to debug.

```
A `gdb:invalid-object-error` exception is thrown if `progspace` is invalid.
```

```
<!-- -->
```

Scheme Procedure: **progspace-objfiles** *progspace*

:   Return the list of objfiles of `progspace`. The order of objfiles in the result is arbitrary. Each element is an object of type `<gdb:objfile>`. See [Objfiles In Guile](Objfiles-In-Guile.html#Objfiles-In-Guile).

```
A `gdb:invalid-object-error` exception is thrown if `progspace` is invalid.
```

```
<!-- -->
```

Scheme Procedure: **progspace-pretty-printers** *progspace*

:   Return the list of pretty-printers of `progspace`. Each element is an object of type `<gdb:pretty-printer>`. See [Guile Pretty Printing API](Guile-Pretty-Printing-API.html#Guile-Pretty-Printing-API), for more information.

```
<!-- -->
```

Scheme Procedure: **set-progspace-pretty-printers!** *progspace printer-list*

:   Set the list of registered `<gdb:pretty-printer>` objects for `progspace`. See [Guile Pretty Printing API](Guile-Pretty-Printing-API.html#Guile-Pretty-Printing-API), for more information.

---

::: header
Next: [Objfiles In Guile](Objfiles-In-Guile.html#Objfiles-In-Guile)]
:::
