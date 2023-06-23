---
tip: translate by openai@2023-06-23 15:52:38
...
---
description: Xmethod API (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Xmethod API (Debugging with GDB)
lang: en
resource-type: document
title: Xmethod API (Debugging with GDB)
---------------------------------------

::: header
Next: [Writing an Xmethod](Writing-an-Xmethod.html#Writing-an-Xmethod)]
:::

---

#### 23.3.2.14 Xmethod API

The [GDB] Python API provides classes, interfaces and functions to implement, register and manipulate xmethods. See [Xmethods In Python](Xmethods-In-Python.html#Xmethods-In-Python).

> GDB 的 Python API 提供类、接口和函数来实现、注册和操作 xmethods。请参见 [Python 中的 Xmethods](Xmethods-In-Python.html#Xmethods-In-Python)。

An xmethod matcher should be an instance of a class derived from `XMethodMatcher` defined in the module `gdb.xmethod`, or an object with similar interface and attributes. An instance of `XMethodMatcher` has the following attributes:

> 一个 xmethod 匹配器应该是从模块 gdb.xmethod 中定义的 XMethodMatcher 类派生的类的实例，或者是具有类似接口和属性的对象。XMethodMatcher 的实例具有以下属性：

Variable: **name**

:   The name of the matcher.

> 名称匹配者。

```

```

Variable: **enabled**

:   A boolean value indicating whether the matcher is enabled or disabled.

> 一个布尔值，指示匹配器是否已启用或禁用。

```

```

Variable: **methods**

:   A list of named methods managed by the matcher. Each object in the list is an instance of the class `XMethod` defined in the module `gdb.xmethod`, or any object with the following attributes:

> 一个由匹配器管理的命名方法列表。列表中的每个对象都是模块 `gdb.xmethod` 中定义的 `XMethod` 类的一个实例，或者具有以下属性的任何对象：

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

> `XMethodMatcher` 类具有以下方法：

Function: **XMethodMatcher.__init__** *(self, name)*

> 函数：**XMethodMatcher.__init__** *（self，name）*

:   Constructs an enabled xmethod matcher with name `name`. The `methods` attribute is initialized to `None`.

> 构造一个名为 `name` 的启用的 xmethod 匹配器。`methods` 属性初始化为 `None`。

```

```

Function: **XMethodMatcher.match** *(self, class_type, method_name)*

> 函数：**XMethodMatcher.match** *（self，class_type，method_name）*

:   Derived classes should override this method. It should return a xmethod worker object (or a sequence of xmethod worker objects) matching the `class_type` is a string value. If the matcher manages named methods as listed in its `methods` attribute, then only those worker objects whose corresponding entries in the `methods` list are enabled should be returned.

> 派生类应该重写此方法。它应该返回一个与 `class_type` 字符串值匹配的 xmethod worker 对象（或一系列 xmethod worker 对象）。如果匹配器管理其 `methods` 属性列出的命名方法，则只应返回其 `methods` 列表中对应条目已启用的工作者对象。

An xmethod worker should be an instance of a class derived from `XMethodWorker` defined in the module `gdb.xmethod`, or support the following interface:

> 应该使用模块 `gdb.xmethod` 中定义的 `XMethodWorker` 类派生出的实例作为 xmethod 工作者，或者支持以下接口：

Function: **XMethodWorker.get_arg_types** *(self)*

> 功能：**XMethodWorker.get_arg_types** *（自我）*

:   This method returns a sequence of `gdb.Type` objects corresponding to the arguments that the xmethod takes. It can return an empty sequence or `None` if the xmethod does not take any arguments. If the xmethod takes a single argument, then a single `gdb.Type` object corresponding to it can be returned.

> 此方法返回一系列 `gdb.Type` 对象，对应于 xmethod 所接受的参数。如果 xmethod 不接受任何参数，则可以返回一个空序列或 `None`。如果 xmethod 只接受一个参数，则可以返回一个对应该参数的 `gdb.Type` 对象。

```

```

Function: **XMethodWorker.get_result_type** *(self, \*args)*

> 函数：**XMethodWorker.get_result_type** *（self，\*args）*
> 获取结果类型

:   This method returns a `gdb.Type` object representing the type of the result of invoking this xmethod. The `args` argument is the same tuple of arguments that would be passed to the `__call__` method of this worker.

> 这种方法返回一个 `gdb.Type` 对象，表示调用此 xmethod 的结果的类型。`args` 参数是将要传递给此工作者的 `__call__` 方法的相同元组参数。

```

```

Function: **XMethodWorker.__call__** *(self, \*args)*

> 函数：**XMethodWorker.__call__** *（自身，\*参数）*

:   This is the method which does the *work* of the xmethod. The `args` arguments is the tuple of arguments to the xmethod. Each element in this tuple is a gdb.Value object. The first element is always the `this` pointer value.

> 这是一种方法，它执行 xmethod 的工作。`args` 参数是 xmethod 的元组参数。该元组中的每个元素都是 gdb.Value 对象。第一个元素总是 `this` 指针值。

For [GDB] to lookup xmethods, the xmethod matchers should be registered using the following function defined in the module `gdb.xmethod`:

> 对于 GDB 来查找 xmethods，应使用模块 gdb.xmethod 中定义的以下函数注册 xmethod 匹配器：

Function: **register_xmethod_matcher** *(locus, matcher, replace=False)*

> 函数：**register_xmethod_matcher** *（位置，匹配器，替换= False）*

:   The `matcher` is registered with `locus`, replacing an existing matcher with the same name as `matcher` if `replace` is `True`. `locus` can be a `gdb.Objfile` object (see [Objfiles In Python](Objfiles-In-Python.html#Objfiles-In-Python)), or a `gdb.Progspace` object (see [Progspaces In Python](Progspaces-In-Python.html#Progspaces-In-Python)), or `None`. If it is `None`, then `matcher` is registered globally.

> 如果 replace 为 True，matcher 将会被注册到 locus，替换掉已存在的使用同样名称的 matcher。locus 可以是 gdb.Objfile 对象（参见 [Python 中的 Objfiles](Objfiles-In-Python.html#Objfiles-In-Python)），或者是 gdb.Progspace 对象（参见 [Python 中的 Progspaces](Progspaces-In-Python.html#Progspaces-In-Python)），或者是 None。如果是 None，那么 matcher 会被全局注册。

---

::: header
Next: [Writing an Xmethod](Writing-an-Xmethod.html#Writing-an-Xmethod)]
:::
