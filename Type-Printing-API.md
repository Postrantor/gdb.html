---
description: Type Printing API (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Type Printing API (Debugging with GDB)
lang: en
resource-type: document
title: Type Printing API (Debugging with GDB)
---
::: header
Next: [Frame Filter API](Frame-Filter-API.html#Frame-Filter-API)]
:::

---

#### 23.3.2.8 Type Printing API

[GDB] provides a way for Python code to customize type display. This is mainly useful for substituting canonical typedef names for types.

A *type printer* is just a Python object conforming to a certain protocol. A simple base class implementing the protocol is provided; see [gdb.types](gdb_002etypes.html#gdb_002etypes). A type printer must supply at least:

Instance Variable of type_printer: **enabled**

:   A boolean which is True if the printer is enabled, and False otherwise. This is manipulated by the `enable type-printer` and `disable type-printer` commands.

```
<!-- -->
```

Instance Variable of type_printer: **name**

:   The name of the type printer. This must be a string. This is used by the `enable type-printer` and `disable type-printer` commands.

```
<!-- -->
```

Method on type_printer: **instantiate** *(self)*

:   This is called by [GDB] at the start of type-printing. It is only called if the type printer is enabled. This method must return a new object that supplies a `recognize` method, as described below.

When displaying a type, say via the `ptype` command, [GDB] will compute a list of type recognizers. This is done by iterating first over the per-objfile type printers (see [Objfiles In Python](Objfiles-In-Python.html#Objfiles-In-Python)), followed by the per-progspace type printers (see [Progspaces In Python](Progspaces-In-Python.html#Progspaces-In-Python)), and finally the global type printers.

[GDB] will call the `instantiate` method of each enabled type printer. If this method returns `None`, then the result is ignored; otherwise, it is appended to the list of recognizers.

Then, when [GDB] is going to display a type name, it iterates over the list of recognizers. For each one, it calls the recognition function, stopping if the function returns a non-`None` value. The recognition function is defined as:

Method on type_recognizer: **recognize** *(self, type)*

:   If `type` argument will be an instance of `gdb.Type` (see [Types In Python](Types-In-Python.html#Types-In-Python)).

[GDB] uses this two-pass approach so that type printers can efficiently cache information without holding on to it too long. For example, it can be convenient to look up type information in a type printer and hold it for a recognizer's lifetime; if a single pass were done then type printers would have to make use of the event system in order to avoid holding information that could become stale as the inferior changed.

---

::: header
Next: [Frame Filter API](Frame-Filter-API.html#Frame-Filter-API)]
:::
