---
description: Python API (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Python API (Debugging with GDB)
lang: en
resource-type: document
title: Python API (Debugging with GDB)
---
::: header
Next: [Python Auto-loading](Python-Auto_002dloading.html#Python-Auto_002dloading)]
:::

---

#### 23.3.2 Python API

You can get quick online help for [GDB].

Functions and methods which have two or more optional arguments allow them to be specified using keyword syntax. This allows passing some optional arguments while skipping others. Example: `gdb.some_function ('foo', bar = 1, baz = 2)`.

---

• [Basic Python](Basic-Python.html#Basic-Python):                                                       Basic Python Functions.
• [Exception Handling](Exception-Handling.html#Exception-Handling):                                     How Python exceptions are translated.
• [Values From Inferior](Values-From-Inferior.html#Values-From-Inferior):                               Python representation of values.
• [Types In Python](Types-In-Python.html#Types-In-Python):                                              Python representation of types.
• [Pretty Printing API](Pretty-Printing-API.html#Pretty-Printing-API):                                  Pretty-printing values.
• [Selecting Pretty-Printers](Selecting-Pretty_002dPrinters.html#Selecting-Pretty_002dPrinters):        How GDB chooses a pretty-printer.
• [Writing a Pretty-Printer](Writing-a-Pretty_002dPrinter.html#Writing-a-Pretty_002dPrinter):           Writing a Pretty-Printer.
• [Type Printing API](Type-Printing-API.html#Type-Printing-API):                                        Pretty-printing types.
• [Frame Filter API](Frame-Filter-API.html#Frame-Filter-API):                                           Filtering Frames.
• [Frame Decorator API](Frame-Decorator-API.html#Frame-Decorator-API):                                                 Decorating Frames.
• [Writing a Frame Filter](Writing-a-Frame-Filter.html#Writing-a-Frame-Filter):                                        Writing a Frame Filter.
• [Unwinding Frames in Python](Unwinding-Frames-in-Python.html#Unwinding-Frames-in-Python):                            Writing frame unwinder.
• [Xmethods In Python](Xmethods-In-Python.html#Xmethods-In-Python):                                                    Adding and replacing methods of C++ classes.
• [Xmethod API](Xmethod-API.html#Xmethod-API):                                                                         Xmethod types.
• [Writing an Xmethod](Writing-an-Xmethod.html#Writing-an-Xmethod):                                                    Writing an xmethod.
• [Inferiors In Python](Inferiors-In-Python.html#Inferiors-In-Python):                                                 Python representation of inferiors (processes)
• [Events In Python](Events-In-Python.html#Events-In-Python):                                                          Listening for events from [GDB].
• [Threads In Python](Threads-In-Python.html#Threads-In-Python):                                                       Accessing inferior threads from Python.
• [Recordings In Python](Recordings-In-Python.html#Recordings-In-Python):                                              Accessing recordings from Python.
• [CLI Commands In Python](CLI-Commands-In-Python.html#CLI-Commands-In-Python):                                        Implementing new CLI commands in Python.
• [GDB/MI Commands In Python](GDB_002fMI-Commands-In-Python.html#GDB_002fMI-Commands-In-Python):                       Implementing new [GDB/MI] commands in Python.
• [Parameters In Python](Parameters-In-Python.html#Parameters-In-Python):                                              Adding new [GDB] parameters.
• [Functions In Python](Functions-In-Python.html#Functions-In-Python):                                                 Writing new convenience functions.
• [Progspaces In Python](Progspaces-In-Python.html#Progspaces-In-Python):                                              Program spaces.
• [Objfiles In Python](Objfiles-In-Python.html#Objfiles-In-Python):                                                    Object files.
• [Frames In Python](Frames-In-Python.html#Frames-In-Python):                                                          Accessing inferior stack frames from Python.
• [Blocks In Python](Blocks-In-Python.html#Blocks-In-Python):                                                          Accessing blocks from Python.
• [Symbols In Python](Symbols-In-Python.html#Symbols-In-Python):                                                       Python representation of symbols.
• [Symbol Tables In Python](Symbol-Tables-In-Python.html#Symbol-Tables-In-Python):                                     Python representation of symbol tables.
• [Line Tables In Python](Line-Tables-In-Python.html#Line-Tables-In-Python):                                           Python representation of line tables.
• [Breakpoints In Python](Breakpoints-In-Python.html#Breakpoints-In-Python):                                           Manipulating breakpoints using Python.
• [Finish Breakpoints in Python](Finish-Breakpoints-in-Python.html#Finish-Breakpoints-in-Python):                      Setting Breakpoints on function return using Python.
• [Lazy Strings In Python](Lazy-Strings-In-Python.html#Lazy-Strings-In-Python):                                        Python representation of lazy strings.
• [Architectures In Python](Architectures-In-Python.html#Architectures-In-Python):                                     Python representation of architectures.
• [Registers In Python](Registers-In-Python.html#Registers-In-Python):                                                 Python representation of registers.
• [Connections In Python](Connections-In-Python.html#Connections-In-Python):                                           Python representation of connections.
• [TUI Windows In Python](TUI-Windows-In-Python.html#TUI-Windows-In-Python):                                           Implementing new TUI windows.
• [Disassembly In Python](Disassembly-In-Python.html#Disassembly-In-Python):                                           Instruction Disassembly In Python

---

---

::: header
Next: [Python Auto-loading](Python-Auto_002dloading.html#Python-Auto_002dloading)]
:::
