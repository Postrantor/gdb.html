---
description: Selecting Pretty-Printers (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Selecting Pretty-Printers (Debugging with GDB)
lang: en
resource-type: document
title: Selecting Pretty-Printers (Debugging with GDB)
---
::: header
Next: [Writing a Pretty-Printer](Writing-a-Pretty_002dPrinter.html#Writing-a-Pretty_002dPrinter)]
:::

---

#### 23.3.2.6 Selecting Pretty-Printers

[GDB] provides several ways to register a pretty-printer: globally, per program space, and per objfile. When choosing how to register your pretty-printer, a good rule is to register it with the smallest scope possible: that is prefer a specific objfile first, then a program space, and only register a printer globally as a last resort.

Variable: **gdb.pretty_printers**

:   The Python list `gdb.pretty_printers` contains an array of functions or callable objects that have been registered via addition as a pretty-printer. Printers in this list are called `global` printers, they're available when debugging all inferiors.

Each `gdb.Progspace` contains a `pretty_printers` attribute. Each `gdb.Objfile` also contains a `pretty_printers` attribute.

Each function on these lists is passed a single `gdb.Value` argument and should return a pretty-printer object conforming to the interface definition above (see [Pretty Printing API](Pretty-Printing-API.html#Pretty-Printing-API)). If a function cannot create a pretty-printer for the value, it should return `None`.

[GDB] then searches the pretty-printer list of the current program space, calling each enabled function until an object is returned. After these lists have been exhausted, it tries the global `gdb.pretty_printers` list, again calling each enabled function until an object is returned.

The order in which the objfiles are searched is not specified. For a given list, functions are always invoked from the head of the list, and iterated over sequentially until the end of the list, or a printer object is returned.

For various reasons a pretty-printer may not work. For example, the underlying data structure may have changed and the pretty-printer is out of date.

The consequences of a broken pretty-printer are severe enough that [GDB] provides support for enabling and disabling individual printers. For example, if `print frame-arguments` is on, a backtrace can become highly illegible if any argument is printed with a broken printer.

Pretty-printers are enabled and disabled by attaching an `enabled` attribute to the registered function or callable object. If this attribute is present and its value is `False`, the printer is disabled, otherwise the printer is enabled.

---

::: header
Next: [Writing a Pretty-Printer](Writing-a-Pretty_002dPrinter.html#Writing-a-Pretty_002dPrinter)]
:::
