---
tip: translate by openai@2023-06-23 12:39:53
...
---
description: Selecting Pretty-Printers (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Selecting Pretty-Printers (Debugging with GDB)
lang: en
resource-type: document
title: Selecting Pretty-Printers (Debugging with GDB)
-----------------------------------------------------

::: header
Next: [Writing a Pretty-Printer](Writing-a-Pretty_002dPrinter.html#Writing-a-Pretty_002dPrinter)]
:::

---

#### 23.3.2.6 Selecting Pretty-Printers

[GDB] provides several ways to register a pretty-printer: globally, per program space, and per objfile. When choosing how to register your pretty-printer, a good rule is to register it with the smallest scope possible: that is prefer a specific objfile first, then a program space, and only register a printer globally as a last resort.

> GDB 提供几种注册美化打印机的方法：全局，每个程序空间和每个 objfile。在选择如何注册您的美化打印机时，一个好的规则是尽可能使用最小的范围注册它：也就是优先选择特定的 objfile，然后是程序空间，最后只作为最后的手段在全局范围注册打印机。

Variable: **gdb.pretty_printers**

> 变量：**gdb.pretty_printers**

:   The Python list `gdb.pretty_printers` contains an array of functions or callable objects that have been registered via addition as a pretty-printer. Printers in this list are called `global` printers, they're available when debugging all inferiors.

> gdb.pretty_printers 列表包含一组通过添加注册的可调用对象或函数。此列表中的打印机被称为“全局”打印机，它们在调试所有子级时可用。

Each `gdb.Progspace` contains a `pretty_printers` attribute. Each `gdb.Objfile` also contains a `pretty_printers` attribute.

> 每个 `gdb.Progspace` 都包含一个 `pretty_printers` 属性。每个 `gdb.Objfile` 也包含一个 `pretty_printers` 属性。

Each function on these lists is passed a single `gdb.Value` argument and should return a pretty-printer object conforming to the interface definition above (see [Pretty Printing API](Pretty-Printing-API.html#Pretty-Printing-API)). If a function cannot create a pretty-printer for the value, it should return `None`.

> 每个函数在这些列表中都会接收一个 `gdb.Value` 参数，并应返回一个符合上面接口定义的美化打印器对象（参见[美化打印 API](Pretty-Printing-API.html#Pretty-Printing-API)）。如果函数不能为该值创建美化打印器，则应返回 `None`。

[GDB] then searches the pretty-printer list of the current program space, calling each enabled function until an object is returned. After these lists have been exhausted, it tries the global `gdb.pretty_printers` list, again calling each enabled function until an object is returned.

> GDB 首先搜索当前程序空间的格式化输出列表，调用每个启用的函数，直到返回一个对象。在这些列表用尽之后，它会尝试全局的 `gdb.pretty_printers` 列表，再次调用每个启用的函数，直到返回一个对象。

The order in which the objfiles are searched is not specified. For a given list, functions are always invoked from the head of the list, and iterated over sequentially until the end of the list, or a printer object is returned.

> 顺序搜索 objfiles 没有规定。对于给定的列表，函数总是从列表头调用，并顺序迭代到列表末尾，或者返回一个打印对象。

For various reasons a pretty-printer may not work. For example, the underlying data structure may have changed and the pretty-printer is out of date.

> 由于各种原因，美化程序可能无法正常工作。例如，底层数据结构可能发生了变化，而美化程序已经过时了。

The consequences of a broken pretty-printer are severe enough that [GDB] provides support for enabling and disabling individual printers. For example, if `print frame-arguments` is on, a backtrace can become highly illegible if any argument is printed with a broken printer.

> 破损的格式化打印机的后果非常严重，以至于[GDB]提供了启用和禁用单个打印机的支持。例如，如果 `print frame-arguments` 处于打开状态，如果使用破损的打印机打印任何参数，回溯将变得非常不清晰。

Pretty-printers are enabled and disabled by attaching an `enabled` attribute to the registered function or callable object. If this attribute is present and its value is `False`, the printer is disabled, otherwise the printer is enabled.

> 美化打印机可以通过将“enabled”属性附加到已注册的函数或可调用对象来启用和禁用。如果此属性存在且其值为“False”，则打印机被禁用，否则打印机被启用。

---

::: header
Next: [Writing a Pretty-Printer](Writing-a-Pretty_002dPrinter.html#Writing-a-Pretty_002dPrinter)]
:::
