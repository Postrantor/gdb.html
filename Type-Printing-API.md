---
tip: translate by openai@2023-06-23 15:00:18
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

> GDB提供了一种方式，让Python代码自定义类型显示。这主要对替换规范类型定义名称的类型很有用。


A *type printer* is just a Python object conforming to a certain protocol. A simple base class implementing the protocol is provided; see [gdb.types](gdb_002etypes.html#gdb_002etypes). A type printer must supply at least:

> 一个*类型打印机*只是一个符合某种协议的Python对象。提供了一个实现该协议的简单基类; 请参阅[gdb.types](gdb_002etypes.html#gdb_002etypes)。类型打印机至少必须提供：


Instance Variable of type_printer: **enabled**

> 实例变量 type_printer 的状态为：**已启用**


:   A boolean which is True if the printer is enabled, and False otherwise. This is manipulated by the `enable type-printer` and `disable type-printer` commands.

> 一个布尔值，如果打印机已启用则为True，否则为False。这可以通过“启用type-printer”和“禁用type-printer”命令来操作。

```

```


Instance Variable of type_printer: **name**

> 实例变量类型_打印机：**名称**


:   The name of the type printer. This must be a string. This is used by the `enable type-printer` and `disable type-printer` commands.

> 名称类型的打印机。这必须是一个字符串。这被`enable type-printer`和`disable type-printer`命令使用。

```

```


Method on type_printer: **instantiate** *(self)*

> 在type_printer上的方法：**实例化** *（自身）*


:   This is called by [GDB] at the start of type-printing. It is only called if the type printer is enabled. This method must return a new object that supplies a `recognize` method, as described below.

> 这是由[GDB]在类型打印开始时调用的。只有在启用类型打印机时才会调用此方法。此方法必须返回一个提供如下所述的`recognize`方法的新对象。


When displaying a type, say via the `ptype` command, [GDB] will compute a list of type recognizers. This is done by iterating first over the per-objfile type printers (see [Objfiles In Python](Objfiles-In-Python.html#Objfiles-In-Python)), followed by the per-progspace type printers (see [Progspaces In Python](Progspaces-In-Python.html#Progspaces-In-Python)), and finally the global type printers.

> 当通过`ptype`命令显示一种类型时，[GDB]将计算一个类型识别器列表。这是通过首先迭代每个objfile类型打印机（参见[Python中的Objfiles](Objfiles-In-Python.html#Objfiles-In-Python)），然后是每个progspace类型打印机（参见[Python中的Progspaces](Progspaces-In-Python.html#Progspaces-In-Python)），最后是全局类型打印机来完成的。


[GDB] will call the `instantiate` method of each enabled type printer. If this method returns `None`, then the result is ignored; otherwise, it is appended to the list of recognizers.

> 如果启用了类型打印机，[GDB] 将调用其 `instantiate` 方法。如果该方法返回 `None`，则忽略结果；否则，将其附加到识别器列表中。


Then, when [GDB] is going to display a type name, it iterates over the list of recognizers. For each one, it calls the recognition function, stopping if the function returns a non-`None` value. The recognition function is defined as:

> 然后，当GDB准备显示一个类型名称时，它会迭代识别器列表。对于每一个，它都会调用识别函数，如果函数返回一个非空值就停止。识别函数定义如下：


Method on type_recognizer: **recognize** *(self, type)*

> 方法在type_recognizer上：**识别** *（自身，类型）*


:   If `type` argument will be an instance of `gdb.Type` (see [Types In Python](Types-In-Python.html#Types-In-Python)).

> 如果`type`参数是一个`gdb.Type`实例（参见[Python中的类型](Types-In-Python.html#Types-In-Python)）。


[GDB] uses this two-pass approach so that type printers can efficiently cache information without holding on to it too long. For example, it can be convenient to look up type information in a type printer and hold it for a recognizer's lifetime; if a single pass were done then type printers would have to make use of the event system in order to avoid holding information that could become stale as the inferior changed.

> [GDB]使用这种双阶段方法，这样类型打印机就可以有效地缓存信息，而不会保留太久。例如，在类型打印机中查找类型信息并将其保留到识别器的生命周期中可能很方便；如果只进行一次通过，那么类型打印机就必须利用事件系统来避免保留可能随着下级改变而变得过时的信息。

---

::: header
Next: [Frame Filter API](Frame-Filter-API.html#Frame-Filter-API)]
:::
