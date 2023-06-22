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

An xmethod matcher should be an instance of a class derived from `XMethodMatcher` defined in the module `gdb.xmethod`, or an object with similar interface and attributes. An instance of `XMethodMatcher` has the following attributes:

Variable: **name**

:   The name of the matcher.

```
<!-- -->
```

Variable: **enabled**

:   A boolean value indicating whether the matcher is enabled or disabled.

```
<!-- -->
```

Variable: **methods**

:   A list of named methods managed by the matcher. Each object in the list is an instance of the class `XMethod` defined in the module `gdb.xmethod`, or any object with the following attributes:

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

```
<!-- -->
```

Function: **XMethodMatcher.match** *(self, class_type, method_name)*

:   Derived classes should override this method. It should return a xmethod worker object (or a sequence of xmethod worker objects) matching the `class_type` is a string value. If the matcher manages named methods as listed in its `methods` attribute, then only those worker objects whose corresponding entries in the `methods` list are enabled should be returned.

An xmethod worker should be an instance of a class derived from `XMethodWorker` defined in the module `gdb.xmethod`, or support the following interface:

Function: **XMethodWorker.get_arg_types** *(self)*

:   This method returns a sequence of `gdb.Type` objects corresponding to the arguments that the xmethod takes. It can return an empty sequence or `None` if the xmethod does not take any arguments. If the xmethod takes a single argument, then a single `gdb.Type` object corresponding to it can be returned.

```
<!-- -->
```

Function: **XMethodWorker.get_result_type** *(self, \*args)*

:   This method returns a `gdb.Type` object representing the type of the result of invoking this xmethod. The `args` argument is the same tuple of arguments that would be passed to the `__call__` method of this worker.

```
<!-- -->
```

Function: **XMethodWorker.__call__** *(self, \*args)*

:   This is the method which does the *work* of the xmethod. The `args` arguments is the tuple of arguments to the xmethod. Each element in this tuple is a gdb.Value object. The first element is always the `this` pointer value.

For [GDB] to lookup xmethods, the xmethod matchers should be registered using the following function defined in the module `gdb.xmethod`:

Function: **register_xmethod_matcher** *(locus, matcher, replace=False)*

:   The `matcher` is registered with `locus`, replacing an existing matcher with the same name as `matcher` if `replace` is `True`. `locus` can be a `gdb.Objfile` object (see [Objfiles In Python](Objfiles-In-Python.html#Objfiles-In-Python)), or a `gdb.Progspace` object (see [Progspaces In Python](Progspaces-In-Python.html#Progspaces-In-Python)), or `None`. If it is `None`, then `matcher` is registered globally.

---

::: header
Next: [Writing an Xmethod](Writing-an-Xmethod.html#Writing-an-Xmethod)]
:::
