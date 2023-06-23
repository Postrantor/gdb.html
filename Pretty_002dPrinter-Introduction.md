---
description: Pretty-Printer Introduction (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Pretty-Printer Introduction (Debugging with GDB)
lang: en
resource-type: document
title: Pretty-Printer Introduction (Debugging with GDB)
---
::: header
Next: [Pretty-Printer Example](Pretty_002dPrinter-Example.html#Pretty_002dPrinter-Example)]
:::

---

#### 10.10.1 Pretty-Printer Introduction

When [GDB] invokes the pretty-printer to print the value. Otherwise the value is printed normally.

Pretty-printers are normally named. This makes them easy to manage. The '`info pretty-printer`.

Pretty-printers are installed by *registering* them with [GDB]. Typically they are automatically loaded and registered when the corresponding debug information is loaded, thus making them available without having to do anything special.

There are three places where a pretty-printer can be registered.

- Pretty-printers registered globally are available when debugging all inferiors.
- Pretty-printers registered with a program space are available only when debugging that program. See [Progspaces In Python](Progspaces-In-Python.html#Progspaces-In-Python), for more details on program spaces in Python.
- Pretty-printers registered with an objfile are loaded and unloaded with the corresponding objfile (e.g., shared library). See [Objfiles In Python](Objfiles-In-Python.html#Objfiles-In-Python), for more details on objfiles in Python.

See [Selecting Pretty-Printers](Selecting-Pretty_002dPrinters.html#Selecting-Pretty_002dPrinters), for further information on how pretty-printers are selected,

See [Writing a Pretty-Printer](Writing-a-Pretty_002dPrinter.html#Writing-a-Pretty_002dPrinter), for implementing pretty printers for new types.
