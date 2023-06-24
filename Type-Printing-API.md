---
tip: translate by openai@2023-06-24 04:20:59
...
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

> GDB 提供了一种方式，让 Python 代码可以自定义类型显示。这主要用于将规范的 typedef 名称替换为类型。


A *type printer* is just a Python object conforming to a certain protocol. A simple base class implementing the protocol is provided; see [gdb.types](gdb_002etypes.html#gdb_002etypes). A type printer must supply at least:

> 一个*类型打印机*只是一个符合某种协议的Python对象。提供了一个实现该协议的基本类；请参见[gdb.types](gdb_002etypes.html#gdb_002etypes)。类型打印机至少需要提供：

Instance Variable of type_printer: **enabled**


:   A boolean which is True if the printer is enabled, and False otherwise. This is manipulated by the `enable type-printer` and `disable type-printer` commands.

> 一个布尔值，如果打印机启用则为True，否则为False。这可以通过“启用类型打印机”和“禁用类型打印机”命令来操作。

```
<!-- -->
```

Instance Variable of type_printer: **name**


:   The name of the type printer. This must be a string. This is used by the `enable type-printer` and `disable type-printer` commands.

> 名称类型的打印机。这必须是一个字符串。这被`enable type-printer`和`disable type-printer`命令使用。

```
<!-- -->
```

Method on type_printer: **instantiate** *(self)*


:   This is called by [GDB] at the start of type-printing. It is only called if the type printer is enabled. This method must return a new object that supplies a `recognize` method, as described below.

> 这被称为[GDB]在类型打印开始时调用。只有在类型打印机启用时才会调用它。此方法必须返回一个新对象，该对象提供如下所述的`recognize`方法。


When displaying a type, say via the `ptype` command, [GDB] will compute a list of type recognizers. This is done by iterating first over the per-objfile type printers (see [Objfiles In Python](Objfiles-In-Python.html#Objfiles-In-Python)), followed by the per-progspace type printers (see [Progspaces In Python](Progspaces-In-Python.html#Progspaces-In-Python)), and finally the global type printers.

> 当通过`ptype`命令显示一种类型时，[GDB]将计算一系列类型识别程序。这是通过首先迭代每个objfile类型打印机（参见[Python中的Objfiles](Objfiles-In-Python.html#Objfiles-In-Python))，然后是每个progspace类型打印机（参见[Python中的Progspaces](Progspaces-In-Python.html#Progspaces-In-Python))，最后是全局类型打印机来实现的。


[GDB] will call the `instantiate` method of each enabled type printer. If this method returns `None`, then the result is ignored; otherwise, it is appended to the list of recognizers.

> [GDB] 将调用每个启用类型打印机的`instantiate`方法。 如果此方法返回`None`，则忽略结果；否则，将其附加到识别器列表中。


Then, when [GDB] is going to display a type name, it iterates over the list of recognizers. For each one, it calls the recognition function, stopping if the function returns a non-`None` value. The recognition function is defined as:

> 当GDB要显示类型名称时，它会遍历识别器列表。对每一个，它都会调用识别函数，如果函数返回非None值则停止。识别函数定义为：

Method on type_recognizer: **recognize** *(self, type)*


:   If `type` argument will be an instance of `gdb.Type` (see [Types In Python](Types-In-Python.html#Types-In-Python)).

> 如果`type`参数是`gdb.Type`的实例（请参阅[Python中的类型](Types-In-Python.html#Types-In-Python)）。


[GDB] uses this two-pass approach so that type printers can efficiently cache information without holding on to it too long. For example, it can be convenient to look up type information in a type printer and hold it for a recognizer's lifetime; if a single pass were done then type printers would have to make use of the event system in order to avoid holding information that could become stale as the inferior changed.

> [GDB] 使用这种双阶段方法，以便类型打印机可以有效地缓存信息而不长期保留它。例如，在类型打印机中查找类型信息，并将其保留到识别器的生命周期中是很方便的；如果只进行一次通过，那么类型打印机将不得不使用事件系统来避免保留可能随着下级变化而变得过时的信息。

---

::: header
Next: [Frame Filter API](Frame-Filter-API.html#Frame-Filter-API)]
:::
