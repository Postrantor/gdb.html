---
description: Selecting Guile Pretty-Printers (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Selecting Guile Pretty-Printers (Debugging with GDB)
lang: en
resource-type: document
title: Selecting Guile Pretty-Printers (Debugging with GDB)
---
::: header
Next: [Writing a Guile Pretty-Printer](Writing-a-Guile-Pretty_002dPrinter.html#Writing-a-Guile-Pretty_002dPrinter)]
:::

---

#### 23.4.3.9 Selecting Guile Pretty-Printers

There are three sets of pretty-printers that [GDB] searches:

- Per-objfile list of pretty-printers (see [Objfiles In Guile](Objfiles-In-Guile.html#Objfiles-In-Guile)).
- Per-progspace list of pretty-printers (see [Progspaces In Guile](Progspaces-In-Guile.html#Progspaces-In-Guile)).
- The global list of pretty-printers (see [Guile Pretty Printing API](Guile-Pretty-Printing-API.html#Guile-Pretty-Printing-API)). These printers are available when debugging any inferior.

Pretty-printer lookup is done by passing the value to be printed to the lookup function of each enabled object in turn. Lookup stops when a lookup function returns a non-`#f` value or when the list is exhausted. Lookup functions must return either a `<gdb:pretty-printer-worker>` object or `#f`. Otherwise an exception is thrown.

[GDB] then searches the result of `progspace-pretty-printers` of the current program space, calling each enabled function until a non-`#f` object is returned. After these lists have been exhausted, it tries the global pretty-printers list, obtained with `pretty-printers`, again calling each enabled function until a non-`#f` object is returned.

The order in which the objfiles are searched is not specified. For a given list, functions are always invoked from the head of the list, and iterated over sequentially until the end of the list, or a `<gdb:pretty-printer-worker>` object is returned.

For various reasons a pretty-printer may not work. For example, the underlying data structure may have changed and the pretty-printer is out of date.

The consequences of a broken pretty-printer are severe enough that [GDB] provides support for enabling and disabling individual printers. For example, if `print frame-arguments` is on, a backtrace can become highly illegible if any argument is printed with a broken printer.

Pretty-printers are enabled and disabled from Scheme by calling `set-pretty-printer-enabled!`. See [Guile Pretty Printing API](Guile-Pretty-Printing-API.html#Guile-Pretty-Printing-API).

---

::: header
Next: [Writing a Guile Pretty-Printer](Writing-a-Guile-Pretty_002dPrinter.html#Writing-a-Guile-Pretty_002dPrinter)]
:::
