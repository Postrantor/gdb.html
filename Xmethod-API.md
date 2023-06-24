---
tip: translate by openai@2023-06-24 04:57:36
...
---
description: Xmethod API (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Xmethod API (Debugging with GDB)
lang: en
resource-type: document
title: Xmethod API (Debugging with GDB)
---
::: header
Next: [Writing an Xmethod](Writing-an-Xmethod.html#Writing-an-Xmethod)]
:::

---

#### 23.3.2.14 Xmethod API


The [GDB] Python API provides classes, interfaces and functions to implement, register and manipulate xmethods. See [Xmethods In Python](Xmethods-In-Python.html#Xmethods-In-Python).

> GDB的Python API提供了类、接口和函数来实现、注册和操作xmethods。请参阅[Python中的Xmethods](Xmethods-In-Python.html#Xmethods-In-Python)。


An xmethod matcher should be an instance of a class derived from `XMethodMatcher` defined in the module `gdb.xmethod`, or an object with similar interface and attributes. An instance of `XMethodMatcher` has the following attributes:

> 一个xmethod匹配器应该是从模块gdb.xmethod中定义的XMethodMatcher类派生的类的一个实例，或者一个具有类似接口和属性的对象。XMethodMatcher的一个实例具有以下属性：

Variable: **name**

:   The name of the matcher.

```
<!-- -->
```

Variable: **enabled**


:   A boolean value indicating whether the matcher is enabled or disabled.

> 一个布尔值，指示匹配器是否启用或禁用。

```
<!-- -->
```

Variable: **methods**


:   A list of named methods managed by the matcher. Each object in the list is an instance of the class `XMethod` defined in the module `gdb.xmethod`, or any object with the following attributes:

> 一个由匹配器管理的命名方法列表。列表中的每个对象都是模块`gdb.xmethod`中定义的`XMethod`类的实例，或具有以下属性的任何对象：

```
`name`

:   Name of the xmethod which should be unique for each xmethod managed by the matcher.

`enabled`

:   A boolean value indicating whether the xmethod is enabled or disabled.

The class `XMethod` is a convenience class with same attributes as above along with the following constructor:

Function: **XMethod.__init__** *(self, name)*

:   Constructs an enabled xmethod with name `name`.
```

The `XMethodMatcher` class has the following methods:

Function: **XMethodMatcher.__init__** *(self, name)*


:   Constructs an enabled xmethod matcher with name `name`. The `methods` attribute is initialized to `None`.

> 构造一个名为“name”的启用xmethod匹配器，“methods”属性初始化为“None”。

```
<!-- -->
```

Function: **XMethodMatcher.match** *(self, class_type, method_name)*


:   Derived classes should override this method. It should return a xmethod worker object (or a sequence of xmethod worker objects) matching the `class_type` is a string value. If the matcher manages named methods as listed in its `methods` attribute, then only those worker objects whose corresponding entries in the `methods` list are enabled should be returned.

> 子类应该重写此方法。它应该返回一个与`class_type`字符串值匹配的xmethod worker对象（或一系列xmethod worker对象）。如果匹配器管理其`methods`属性中列出的命名方法，那么只有那些对应`methods`列表中启用的条目的工作者对象才会被返回。


An xmethod worker should be an instance of a class derived from `XMethodWorker` defined in the module `gdb.xmethod`, or support the following interface:

> 一个xmethod工作者应该是模块`gdb.xmethod`中定义的`XMethodWorker`的一个实例，或者支持以下接口：

Function: **XMethodWorker.get_arg_types** *(self)*


:   This method returns a sequence of `gdb.Type` objects corresponding to the arguments that the xmethod takes. It can return an empty sequence or `None` if the xmethod does not take any arguments. If the xmethod takes a single argument, then a single `gdb.Type` object corresponding to it can be returned.

> 此方法返回一系列`gdb.Type`对象，对应于xmethod所接受的参数。如果xmethod不接受任何参数，则可以返回一个空序列或`None`。如果xmethod只接受一个参数，则可以返回一个对应于它的单个`gdb.Type`对象。

```
<!-- -->
```

Function: **XMethodWorker.get_result_type** *(self, \*args)*


:   This method returns a `gdb.Type` object representing the type of the result of invoking this xmethod. The `args` argument is the same tuple of arguments that would be passed to the `__call__` method of this worker.

> 此方法返回一个`gdb.Type`对象，表示调用此xmethod的结果的类型。`args`参数是将传递给此工作程序的`__call__`方法的相同元组参数。

```
<!-- -->
```

Function: **XMethodWorker.__call__** *(self, \*args)*


:   This is the method which does the *work* of the xmethod. The `args` arguments is the tuple of arguments to the xmethod. Each element in this tuple is a gdb.Value object. The first element is always the `this` pointer value.

> 这是一种方法，它完成xmethod的工作。`args`参数是xmethod的元组参数。这个元组中的每个元素都是一个gdb.Value对象。第一个元素总是`this`指针值。


For [GDB] to lookup xmethods, the xmethod matchers should be registered using the following function defined in the module `gdb.xmethod`:

> 若要让GDB查找xmethods，应当使用模块`gdb.xmethod`中定义的以下函数注册xmethod matchers：

Function: **register_xmethod_matcher** *(locus, matcher, replace=False)*


:   The `matcher` is registered with `locus`, replacing an existing matcher with the same name as `matcher` if `replace` is `True`. `locus` can be a `gdb.Objfile` object (see [Objfiles In Python](Objfiles-In-Python.html#Objfiles-In-Python)), or a `gdb.Progspace` object (see [Progspaces In Python](Progspaces-In-Python.html#Progspaces-In-Python)), or `None`. If it is `None`, then `matcher` is registered globally.

> 注册器`matcher`已经被注册到`locus`，如果`replace`设置为`True`，则会替换具有与`matcher`相同名称的现有注册器。`locus`可以是`gdb.Objfile`对象（参见[Python中的Objfiles](Objfiles-In-Python.html#Objfiles-In-Python)）或`gdb.Progspace`对象（参见[Python中的Progspaces](Progspaces-In-Python.html#Progspaces-In-Python)）或`None`。如果它是`None`，那么`matcher`将被全局注册。

---

::: header
Next: [Writing an Xmethod](Writing-an-Xmethod.html#Writing-an-Xmethod)]
:::
