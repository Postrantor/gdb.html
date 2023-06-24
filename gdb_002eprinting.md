---
tip: translate by openai@2023-06-23 21:40:43
...
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

> 这个模块提供了一组用于操作美化打印机的实用程序。

`PrettyPrinter (name, subprinters=None)`


:   This class specifies the API that makes '`info pretty-printer`' work. Pretty-printers should generally inherit from this class.

> 这个类指定了使“信息漂亮打印机”工作的API。漂亮打印机通常应该从这个类继承。

`SubPrettyPrinter (name)`


:   For printers that handle multiple types, this class specifies the corresponding API for the subprinters.

> 对于处理多种类型的打印机，此类指定了子打印机的相应API。

`RegexpCollectionPrettyPrinter (name)`


:   Utility class for handling multiple printers, all recognized via regular expressions. See [Writing a Pretty-Printer](Writing-a-Pretty_002dPrinter.html#Writing-a-Pretty_002dPrinter), for an example.

> 这是一个用于处理多个打印机的实用程序类，所有打印机都是通过正则表达式来识别的。有关示例，请参阅《编写漂亮的打印机》（Writing-a-Pretty_002dPrinter.html#Writing-a-Pretty_002dPrinter）。

`FlagEnumerationPrinter (name)`


:   A pretty-printer which handles printing of `enum` values. Unlike [GDB] is the name of the printer and also the name of the `enum` type to look up.

> 一个处理`枚举`值的漂亮打印机。不像[GDB]是打印机的名字，也是要查找的`枚举`类型的名字。

`register_pretty_printer (obj, printer, replace=False)`


:   Register `printer` is `True` then any existing copy of the printer is replaced. Otherwise a `RuntimeError` exception is raised if a printer with the same name already exists.

> 如果注册打印机为真，那么任何现有的打印机副本都将被替换。如果已经存在同名打印机，则会引发一个RuntimeError异常。
