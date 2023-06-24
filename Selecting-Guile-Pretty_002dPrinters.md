---
tip: translate by openai@2023-06-24 02:21:06
...
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

> - 每个对象文件的可美化打印机列表（参见[Guile中的对象文件](Objfiles-In-Guile.html#Objfiles-In-Guile)）。

- Per-progspace list of pretty-printers (see [Progspaces In Guile](Progspaces-In-Guile.html#Progspaces-In-Guile)).

> - 在Guile中的Progspaces列表中的格式化打印机（参见[Guile中的Progspaces]（Progspaces-In-Guile.html#Progspaces-In-Guile））。

- The global list of pretty-printers (see [Guile Pretty Printing API](Guile-Pretty-Printing-API.html#Guile-Pretty-Printing-API)). These printers are available when debugging any inferior.

> 全局可美化打印列表（参见[Guile Pretty Printing API](Guile-Pretty-Printing-API.html#Guile-Pretty-Printing-API)）。在调试任何次级时，这些打印机都可用。


Pretty-printer lookup is done by passing the value to be printed to the lookup function of each enabled object in turn. Lookup stops when a lookup function returns a non-`#f` value or when the list is exhausted. Lookup functions must return either a `<gdb:pretty-printer-worker>` object or `#f`. Otherwise an exception is thrown.

> 通过将要打印的值传递给启用的每个对象的查找函数，来完成漂亮打印机查找。当查找函数返回非#f值或列表耗尽时，查找就会停止。查找函数必须返回<gdb:pretty-printer-worker>对象或#f。否则将抛出异常。


[GDB] then searches the result of `progspace-pretty-printers` of the current program space, calling each enabled function until a non-`#f` object is returned. After these lists have been exhausted, it tries the global pretty-printers list, obtained with `pretty-printers`, again calling each enabled function until a non-`#f` object is returned.

> GDB 接着会搜索当前程序空间中的`progspace-pretty-printers`的结果，调用每一个已启用的函数，直到返回一个非#f的对象。在这些列表用尽之后，它会尝试使用`pretty-printers`获取的全局pretty-printers列表，再次调用每一个已启用的函数，直到返回一个非#f的对象。


The order in which the objfiles are searched is not specified. For a given list, functions are always invoked from the head of the list, and iterated over sequentially until the end of the list, or a `<gdb:pretty-printer-worker>` object is returned.

> 搜索objfiles的顺序没有特定的规定。对于给定的列表，函数总是从列表头部调用，并且按顺序迭代直到列表的末尾，或者返回一个`<gdb:pretty-printer-worker>`对象。


For various reasons a pretty-printer may not work. For example, the underlying data structure may have changed and the pretty-printer is out of date.

> 因为各种原因，美化程序可能无法正常工作。例如，底层数据结构可能已经改变，而美化程序已经过时了。


The consequences of a broken pretty-printer are severe enough that [GDB] provides support for enabling and disabling individual printers. For example, if `print frame-arguments` is on, a backtrace can become highly illegible if any argument is printed with a broken printer.

> 破损的格式化打印机的后果非常严重，以至于[GDB]提供了支持来启用和禁用单个打印机的功能。例如，如果`print frame-arguments`开启，如果任何参数使用破损的打印机打印，回溯可能变得非常不清晰。


Pretty-printers are enabled and disabled from Scheme by calling `set-pretty-printer-enabled!`. See [Guile Pretty Printing API](Guile-Pretty-Printing-API.html#Guile-Pretty-Printing-API).

> 可以通过调用“set-pretty-printer-enabled!”来在Scheme中启用和禁用可美化打印机。请参阅[Guile Pretty Printing API](Guile-Pretty-Printing-API.html#Guile-Pretty-Printing-API)。

---

::: header
Next: [Writing a Guile Pretty-Printer](Writing-a-Guile-Pretty_002dPrinter.html#Writing-a-Guile-Pretty_002dPrinter)]
:::
