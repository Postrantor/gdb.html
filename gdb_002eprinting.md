---
description: gdb.printing (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: gdb.printing (Debugging with GDB)
lang: en
resource-type: document
title: gdb.printing (Debugging with GDB)
---
::: header
Next: [gdb.types](gdb_002etypes.html#gdb_002etypes)]
:::

---

#### 23.3.4.1 gdb.printing

This module provides a collection of utilities for working with pretty-printers.

`PrettyPrinter (name, subprinters=None)`

:   This class specifies the API that makes '`info pretty-printer`' work. Pretty-printers should generally inherit from this class.

`SubPrettyPrinter (name)`

:   For printers that handle multiple types, this class specifies the corresponding API for the subprinters.

`RegexpCollectionPrettyPrinter (name)`

:   Utility class for handling multiple printers, all recognized via regular expressions. See [Writing a Pretty-Printer](Writing-a-Pretty_002dPrinter.html#Writing-a-Pretty_002dPrinter), for an example.

`FlagEnumerationPrinter (name)`

:   A pretty-printer which handles printing of `enum` values. Unlike [GDB] is the name of the printer and also the name of the `enum` type to look up.

`register_pretty_printer (obj, printer, replace=False)`

:   Register `printer` is `True` then any existing copy of the printer is replaced. Otherwise a `RuntimeError` exception is raised if a printer with the same name already exists.
