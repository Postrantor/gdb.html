---
description: Objfiles In Guile (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Objfiles In Guile (Debugging with GDB)
lang: en
resource-type: document
title: Objfiles In Guile (Debugging with GDB)
---
::: header
Next: [Frames In Guile](Frames-In-Guile.html#Frames-In-Guile)]
:::

---

#### 23.4.3.14 Objfiles In Guile

[GDB] calls these symbol-containing files *objfiles*.

Each objfile is represented as an object of type `<gdb:objfile>`.

The following objfile-related procedures are provided by the `(gdb)` module:

Scheme Procedure: **objfile?** *object*

:   Return `#t` if `object` is a `<gdb:objfile>` object. Otherwise return `#f`.

```
<!-- -->
```

Scheme Procedure: **objfile-valid?** *objfile*

:   Return `#t` if `objfile` any longer. All other `<gdb:objfile>` procedures will throw an exception if it is invalid at the time the procedure is called.

```
<!-- -->
```

Scheme Procedure: **objfile-filename** *objfile*

:   Return the file name of `objfile` as a string, with symbolic links resolved.

```
<!-- -->
```

Scheme Procedure: **objfile-progspace** *objfile*

:   Return the `<gdb:progspace>` that this object file lives in. See [Progspaces In Guile](Progspaces-In-Guile.html#Progspaces-In-Guile), for more on progspaces.

```
<!-- -->
```

Scheme Procedure: **objfile-pretty-printers** *objfile*

:   Return the list of registered `<gdb:pretty-printer>` objects for `objfile`. See [Guile Pretty Printing API](Guile-Pretty-Printing-API.html#Guile-Pretty-Printing-API), for more information.

```
<!-- -->
```

Scheme Procedure: **set-objfile-pretty-printers!** *objfile printer-list*

:   Set the list of registered `<gdb:pretty-printer>` objects for `objfile` must be a list of `<gdb:pretty-printer>` objects. See [Guile Pretty Printing API](Guile-Pretty-Printing-API.html#Guile-Pretty-Printing-API), for more information.

```
<!-- -->
```

Scheme Procedure: **current-objfile**

:   When auto-loading a Guile script (see [Guile Auto-loading](Guile-Auto_002dloading.html#Guile-Auto_002dloading)), [GDB] sets the "current objfile" to the corresponding objfile. This function returns the current objfile. If there is no current objfile, this function returns `#f`.

```
<!-- -->
```

Scheme Procedure: **objfiles**

:   Return a list of all the objfiles in the current program space.

---

::: header
Next: [Frames In Guile](Frames-In-Guile.html#Frames-In-Guile)]
:::
