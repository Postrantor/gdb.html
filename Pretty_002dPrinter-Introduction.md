---
tip: translate by openai@2023-06-24 01:10:52
...
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

> 当GDB调用美化打印机来打印值时，否则值会正常打印。


Pretty-printers are normally named. This makes them easy to manage. The '`info pretty-printer`.

> 美化打印机通常有名字，这使得它们很容易管理。'info pretty-printer'。


Pretty-printers are installed by *registering* them with [GDB]. Typically they are automatically loaded and registered when the corresponding debug information is loaded, thus making them available without having to do anything special.

> 美化打印机通过向GDB注册来安装。通常，当加载相应的调试信息时，它们会自动加载并注册，因此无需做任何特殊操作就可以使用它们。

There are three places where a pretty-printer can be registered.

- Pretty-printers registered globally are available when debugging all inferiors.

- Pretty-printers registered with a program space are available only when debugging that program. See [Progspaces In Python](Progspaces-In-Python.html#Progspaces-In-Python), for more details on program spaces in Python.

> 给程序空间注册的格式化打印只有在调试该程序时才可用。有关Python中的程序空间的更多详细信息，请参阅[Progspaces In Python](Progspaces-In-Python.html#Progspaces-In-Python)。

- Pretty-printers registered with an objfile are loaded and unloaded with the corresponding objfile (e.g., shared library). See [Objfiles In Python](Objfiles-In-Python.html#Objfiles-In-Python), for more details on objfiles in Python.

> 注册到objfile的格式化打印器会随着相应的objfile（例如共享库）的加载和卸载而加载和卸载。有关Python中objfile的更多详细信息，请参见[Python中的Objfiles](Objfiles-In-Python.html#Objfiles-In-Python)。


See [Selecting Pretty-Printers](Selecting-Pretty_002dPrinters.html#Selecting-Pretty_002dPrinters), for further information on how pretty-printers are selected,

> 请参阅[选择美化打印机](Selecting-Pretty_002dPrinters.html#Selecting-Pretty_002dPrinters)，了解有关如何选择美化打印机的更多信息。


See [Writing a Pretty-Printer](Writing-a-Pretty_002dPrinter.html#Writing-a-Pretty_002dPrinter), for implementing pretty printers for new types.

> 请参阅[编写美化打印机](Writing-a-Pretty_002dPrinter.html#Writing-a-Pretty_002dPrinter)，以实现新类型的美化打印机。
