---
tip: translate by openai@2023-06-23 18:16:48
...
---
description: Breakpoints In Python (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Breakpoints In Python (Debugging with GDB)
lang: en
resource-type: document
title: Breakpoints In Python (Debugging with GDB)
---
::: header
Next: [Finish Breakpoints in Python](Finish-Breakpoints-in-Python.html#Finish-Breakpoints-in-Python)]
:::

---

#### 23.3.2.31 Manipulating breakpoints using Python


Python code can manipulate breakpoints via the `gdb.Breakpoint` class.

> Python 代码可以通过`gdb.Breakpoint`类来操纵断点。


A breakpoint can be created using one of the two forms of the `gdb.Breakpoint` constructor. The first one accepts a string like one would pass to the `break` (see [Setting Breakpoints](Set-Breaks.html#Set-Breaks)) and `watch` (see [Setting Watchpoints](Set-Watchpoints.html#Set-Watchpoints)) commands, and can be used to create both breakpoints and watchpoints. The second accepts separate Python arguments similar to [Explicit Locations](Explicit-Locations.html#Explicit-Locations), and can only be used to create breakpoints.

> 可以使用`gdb.Breakpoint`构造函数的两种形式之一创建断点。第一种接受一个字符串，就像传递给`break`（参见[设置断点](Set-Breaks.html#Set-Breaks))和`watch`（参见[设置监视点](Set-Watchpoints.html#Set-Watchpoints))命令一样，可用于创建断点和监视点。第二种接受类似[显式位置](Explicit-Locations.html#Explicit-Locations)的单独的Python参数，只能用于创建断点。

)*


:   Create a new breakpoint according to `spec`, which is a string naming the location of a breakpoint, or an expression that defines a watchpoint. The string should describe a location in a format recognized by the `break` command (see [Setting Breakpoints](Set-Breaks.html#Set-Breaks)) or, in the case of a watchpoint, by the `watch` command (see [Setting Watchpoints](Set-Watchpoints.html#Set-Watchpoints)).

> 根据'spec'（一个描述断点位置的字符串或表达式）创建一个新断点，或者一个表达式定义的监视点。字符串应该描述一个`break`命令（参见[设置断点](Set-Breaks.html#Set-Breaks)）可以识别的格式，或者在监视点的情况下，由`watch`命令（参见[设置监视点](Set-Watchpoints.html#Set-Watchpoints)）识别的格式。

```
The optional `type` argument specifies the type of the breakpoint to create, as defined below.

The optional `wp_class` is omitted, it defaults to `gdb.WP_WRITE`.

The optional `internal` argument allows the breakpoint to become invisible to the user. The breakpoint will neither be reported when created, nor will it be listed in the output from `info breakpoints` (but will be listed with the `maint info breakpoints` command).

The optional `temporary` argument makes the breakpoint a temporary breakpoint. Temporary breakpoints are deleted after they have been hit. Any further access to the Python breakpoint after it has been hit will result in a runtime error (as that breakpoint has now been automatically deleted).

The optional `qualified` argument is a boolean that allows interpreting the function passed in `spec` as a fully-qualified name. It is equivalent to `break`'s `-qualified` flag (see [Linespec Locations](Linespec-Locations.html#Linespec-Locations) and [Explicit Locations](Explicit-Locations.html#Explicit-Locations)).
```

```
<!-- -->
```

)*


:   This second form of creating a new breakpoint specifies the explicit location (see [Explicit Locations](Explicit-Locations.html#Explicit-Locations)) using keywords. The new breakpoint will be created in the specified source file `source`.

> 这种创建新断点的第二种方式使用关键字指定明确的位置（参见[明确位置](Explicit-Locations.html#Explicit-Locations)）。新断点将在指定的源文件`source`中创建。

```
`internal` have the same usage as explained previously.
```


The available types are represented by constants defined in the `gdb` module:

> 可用类型由`gdb`模块中定义的常量表示：

`gdb.BP_BREAKPOINT`

Normal code breakpoint.

`gdb.BP_HARDWARE_BREAKPOINT`


Hardware assisted code breakpoint.

> 硬件辅助代码断点。

`gdb.BP_WATCHPOINT`

Watchpoint breakpoint.

`gdb.BP_HARDWARE_WATCHPOINT`


Hardware assisted watchpoint.

> 硬件辅助监视点。

`gdb.BP_READ_WATCHPOINT`


Hardware assisted read watchpoint.

> 硬件辅助读取监视点。

`gdb.BP_ACCESS_WATCHPOINT`


Hardware assisted access watchpoint.

> 硬件辅助访问监视点。

`gdb.BP_CATCHPOINT`


Catchpoint. Currently, this type can't be used when creating `gdb.Breakpoint` objects, but will be present in `gdb.Breakpoint` objects reported from `gdb.BreakpointEvent` s (see [Events In Python](Events-In-Python.html#Events-In-Python)).

> 捕获点。目前，在创建gdb.Breakpoint对象时无法使用此类型，但将出现在从gdb.BreakpointEvent报告的gdb.Breakpoint对象中（请参见[Python中的事件]（Events-In-Python.html#Events-In-Python））。


The available watchpoint types are represented by constants defined in the `gdb` module:

> `gdb` 模块中定义的常量表示可用的断点类型：

`gdb.WP_READ`

Read only watchpoint.

`gdb.WP_WRITE`

Write only watchpoint.

`gdb.WP_ACCESS`

Read/Write watchpoint.


Function: **Breakpoint.stop** *(self)*

> 功能：**断点.停止**（自身）


:   The `gdb.Breakpoint` class can be sub-classed and, in particular, you may choose to implement the `stop` method. If this method is defined in a sub-class of `gdb.Breakpoint`, it will be called when the inferior reaches any location of a breakpoint which instantiates that sub-class. If the method returns `True`, the inferior will be stopped at the location of the breakpoint, otherwise the inferior will continue.

> 类`gdb.Breakpoint`可以被子类化，特别是你可以选择实现`stop`方法。如果这个方法被定义在`gdb.Breakpoint`的子类中，当次等级的控制流到达任何实例化该子类的断点位置时，它将被调用。如果方法返回`True`，次等级将停止在断点的位置，否则次等级将继续执行。

```
If there are multiple breakpoints at the same location with a `stop` method, each one will be called regardless of the return status of the previous. This ensures that all `stop` methods have a chance to execute at that location. In this scenario if one of the methods returns `True` but the others return `False`, the inferior will still be stopped.

You should not alter the execution state of the inferior (i.e., step, next, etc.), alter the current frame context (i.e., change the current active frame), or alter, add or delete any breakpoint. As a general rule, you should not alter any data within [GDB] or the inferior at this time.

Example `stop` implementation:

::: smallexample
``` smallexample

class MyBreakpoint (gdb.Breakpoint):

> 类MyBreakpoint（gdb.Breakpoint）：
      def stop (self):
        inf_val = gdb.parse_and_eval("foo")
        if inf_val == 3:
          return True
        return False
```

:::

```

```

<!-- -->

```


Function: **Breakpoint.is_valid** *()*

> 函数：**Breakpoint.is_valid** *（）*


:   Return `True` if this `Breakpoint` object is valid, `False` otherwise. A `Breakpoint` object can become invalid if the user deletes the breakpoint. In this case, the object still exists, but the underlying breakpoint does not. In the cases of watchpoint scope, the watchpoint remains valid even if execution of the inferior leaves the scope of that watchpoint.

> 如果这个断点对象有效，则返回“True”，否则返回“False”。如果用户删除了断点，断点对象可能会失效。在这种情况下，对象仍然存在，但底层断点不存在。在监视点范围的情况下，即使下级离开该监视点的范围，监视点仍然有效。

```

<!-- -->

```


Function: **Breakpoint.delete** *()*

> 功能：**Breakpoint.delete** *（）*


:   Permanently deletes the [GDB] breakpoint. This also invalidates the Python `Breakpoint` object. Any further access to this object's attributes or methods will raise an error.

> 永久删除[GDB]断点。这也使Python `Breakpoint`对象失效。任何进一步访问此对象的属性或方法都会引发错误。

```

<!-- -->

```


Variable: **Breakpoint.enabled**

> 变量：**Breakpoint.enabled**


:   This attribute is `True` if the breakpoint is enabled, and `False` otherwise. This attribute is writable. You can use it to enable or disable the breakpoint.

> 这个属性如果断点被启用，则为“True”，否则为“False”。这个属性是可写的。您可以使用它来启用或禁用断点。

```

<!-- -->

```


Variable: **Breakpoint.silent**

> 变量：**Breakpoint.silent**


:   This attribute is `True` if the breakpoint is silent, and `False` otherwise. This attribute is writable.

> 这个属性如果断点是静默的，则为`True`，否则为`False`。这个属性是可写的。

```

Note that a breakpoint can also be silent if it has commands and the first command is `silent`. This is not reported by the `silent` attribute.

```

```

<!-- -->

```


Variable: **Breakpoint.pending**

> 变量：**Breakpoint.pending**


:   This attribute is `True` if the breakpoint is pending, and `False` otherwise. See [Set Breaks](Set-Breaks.html#Set-Breaks). This attribute is read-only.

> 这个属性如果断点是悬而未决的，则为`True`，否则为`False`。请参阅[设置断点](Set-Breaks.html#Set-Breaks)。这个属性是只读的。




Variable: **Breakpoint.thread**

> 变量：**断点线程**


:   If the breakpoint is thread-specific, this attribute holds the thread's global id. If the breakpoint is not thread-specific, this attribute is `None`. This attribute is writable.

> 如果断点是特定于线程的，此属性包含线程的全局ID。如果断点不是特定于线程的，此属性为“None”。此属性可写。

```

<!-- -->

```


Variable: **Breakpoint.task**

> 变量：**断点。任务**


:   If the breakpoint is Ada task-specific, this attribute holds the Ada task id. If the breakpoint is not task-specific (or the underlying language is not Ada), this attribute is `None`. This attribute is writable.

> 如果断点是特定于Ada任务的，此属性包含Ada任务ID。如果断点不是特定于任务的（或底层语言不是Ada），此属性为“无”。此属性可写。

```

<!-- -->

```


Variable: **Breakpoint.ignore_count**

> 变量：**Breakpoint.ignore_count**


:   This attribute holds the ignore count for the breakpoint, an integer. This attribute is writable.

> 这个属性保存断点的忽略计数，是一个整数。这个属性是可写的。

```

<!-- -->

```


Variable: **Breakpoint.number**

> 变量：**断点编号**


:   This attribute holds the breakpoint's number --- the identifier used by the user to manipulate the breakpoint. This attribute is not writable.

> 这个属性保存断点的编号 --- 用户用来操作断点的标识符。这个属性不能写入。

```

<!-- -->

```


Variable: **Breakpoint.type**

> 变量：**断点类型**


:   This attribute holds the breakpoint's type --- the identifier used to determine the actual breakpoint type or use-case. This attribute is not writable.

> 这个属性保存断点的类型---用于确定实际断点类型或用例的标识符。此属性不可写。

```

<!-- -->

```


Variable: **Breakpoint.visible**

> 变量：**Breakpoint.visible**


:   This attribute tells whether the breakpoint is visible to the user when set, or when the '`info breakpoints`' command is run. This attribute is not writable.

> 这个属性告诉我们，当设置断点时，或者运行'info breakpoints'命令时，用户是否可以看到这个断点。这个属性不可写。

```

<!-- -->

```


Variable: **Breakpoint.temporary**

> 变量：**Breakpoint.temporary**


:   This attribute indicates whether the breakpoint was created as a temporary breakpoint. Temporary breakpoints are automatically deleted after that breakpoint has been hit. Access to this attribute, and all other attributes and functions other than the `is_valid` function, will result in an error after the breakpoint has been hit (as it has been automatically deleted). This attribute is not writable.

> 这个属性表明断点是否被作为临时断点创建。临时断点在断点被触及后会自动删除。访问这个属性和其他除`is_valid`函数以外的属性和函数，会在断点被触及后导致错误（因为它已经被自动删除）。这个属性不可写。

```

<!-- -->

```


Variable: **Breakpoint.hit_count**

> 变量：**断点计数**


:   This attribute holds the hit count for the breakpoint, an integer. This attribute is writable, but currently it can only be set to zero.

> 这个属性保存断点的命中次数，一个整数。这个属性是可写的，但目前只能设置为零。

```

<!-- -->

```


Variable: **Breakpoint.location**

> 变量：**断点位置**


:   This attribute holds the location of the breakpoint, as specified by the user. It is a string. If the breakpoint does not have a location (that is, it is a watchpoint) the attribute's value is `None`. This attribute is not writable.

> 这个属性保存了用户指定的断点位置。它是一个字符串。如果断点没有位置（也就是说，它是一个观察点），属性的值为`None`。这个属性是不可写的。

```

<!-- -->

```


Variable: **Breakpoint.locations**

> 变量：**断点位置**


:   Get the most current list of breakpoint locations that are inserted for this breakpoint, with elements of type `gdb.BreakpointLocation` (described below). This functionality matches that of the `info breakpoint` command (see [Set Breaks](Set-Breaks.html#Set-Breaks)), in that it only retrieves the most current list of locations, thus the list itself when returned is not updated behind the scenes. This attribute is not writable.

> 获取最新的断点位置列表，这些断点位置的元素类型为`gdb.BreakpointLocation`（如下所述）。此功能与`info breakpoint`命令（请参阅[Set Breaks](Set-Breaks.html#Set-Breaks)）匹配，因为它仅检索最新的位置列表，因此返回的列表本身不会在后台更新。此属性不可写。

```

<!-- -->

```


Variable: **Breakpoint.expression**

> 变量：**断点表达式**


:   This attribute holds a breakpoint expression, as specified by the user. It is a string. If the breakpoint does not have an expression (the breakpoint is not a watchpoint) the attribute's value is `None`. This attribute is not writable.

> 这个属性保存用户指定的断点表达式，它是一个字符串。如果断点没有表达式（断点不是一个监视点），该属性的值为'None'。这个属性是不可写的。

```

<!-- -->

```


Variable: **Breakpoint.condition**

> 变量：**断点条件**


:   This attribute holds the condition of the breakpoint, as specified by the user. It is a string. If there is no condition, this attribute's value is `None`. This attribute is writable.

> 这个属性保存断点的条件，根据用户指定。它是一个字符串。如果没有条件，这个属性的值为`None`。这个属性是可写的。

```

<!-- -->

```


Variable: **Breakpoint.commands**

> 变量：**Breakpoint.commands**


:   This attribute holds the commands attached to the breakpoint. If there are commands, this attribute's value is a string holding all the commands, separated by newlines. If there are no commands, this attribute is `None`. This attribute is writable.

> 这个属性保存了与断点相关的命令。如果有命令，该属性的值是一个字符串，所有命令用换行符分隔。如果没有命令，此属性为“None”。此属性可写。



#### Breakpoint Locations 


A breakpoint location is one of the actual places where a breakpoint has been set, represented in the Python API by the `gdb.BreakpointLocation` type. This type is never instantiated by the user directly, but is retrieved from `Breakpoint.locations` which returns a list of breakpoint locations where it is currently set. Breakpoint locations can become invalid if new symbol files are loaded or dynamically loaded libraries are closed. Accessing the attributes of an invalidated breakpoint location will throw a `RuntimeError` exception. Access the `Breakpoint.locations` attribute again to retrieve the new and valid breakpoints location list.

> 一个断点位置是设置断点时实际位置之一，在Python API中由`gdb.BreakpointLocation`类型表示。用户不会直接实例化此类型，而是从`Breakpoint.locations`中获取，该属性返回当前设置的断点位置列表。如果加载了新的符号文件或关闭了动态加载的库，断点位置可能会失效。访问失效的断点位置的属性将抛出`RuntimeError`异常。再次访问`Breakpoint.locations`属性以获取新的有效断点位置列表。


Variable: **BreakpointLocation.source**

> 变量：**BreakpointLocation.source**


:   This attribute returns the source file path and line number where this location was set. The type of the attribute is a tuple of `string`. If the breakpoint location doesn't have a source location, it returns None, which is the case for watchpoints and catchpoints. This will throw a `RuntimeError` exception if the location has been invalidated. This attribute is not writable.

> 此属性返回设置此位置的源文件路径和行号。属性的类型为字符串元组。如果断点位置没有源位置，则返回None，这是监视点和捕获点的情况。如果位置无效，则会抛出`RuntimeError`异常。此属性不可写。

```

<!-- -->

```


Variable: **BreakpointLocation.address**

> 变量：**BreakpointLocation.address**


:   This attribute returns the address where this location was set. This attribute is of type long. This will throw a `RuntimeError` exception if the location has been invalidated. This attribute is not writable.

> 此属性返回设置此位置的地址。此属性的类型为long。如果位置已失效，则会抛出`RuntimeError`异常。此属性不可写。

```

<!-- -->

```


Variable: **BreakpointLocation.enabled**

> 变量：**BreakpointLocation.enabled**


:   This attribute holds the value for whether or not this location is enabled. This attribute is writable (boolean). This will throw a `RuntimeError` exception if the location has been invalidated.

> 此属性保存此位置是否启用的值。此属性可写（布尔值）。如果位置已失效，将抛出`RuntimeError`异常。

```

<!-- -->

```


Variable: **BreakpointLocation.owner**

> 变量：**BreakpointLocation.owner**


:   This attribute holds a reference to the `gdb.Breakpoint` owner object, from which this `gdb.BreakpointLocation` was retrieved from. This will throw a `RuntimeError` exception if the location has been invalidated. This attribute is not writable.

> 这个属性保存了一个指向`gdb.Breakpoint`所有者对象的引用，从中获取这个`gdb.BreakpointLocation`。如果位置已经失效，将会抛出一个`RuntimeError`异常。这个属性不可写。

```

<!-- -->

```


Variable: **BreakpointLocation.function**

> 变量：**BreakpointLocation.function**


:   This attribute gets the name of the function where this location was set. If no function could be found this attribute returns `None`. This will throw a `RuntimeError` exception if the location has been invalidated. This attribute is not writable.

> 这个属性获取设置此位置的函数的名称。如果找不到函数，此属性将返回`None`。如果位置被无效，这将抛出`RuntimeError`异常。此属性不可写。

```

<!-- -->

```


Variable: **BreakpointLocation.fullname**

> 变量：**BreakpointLocation.fullname**


:   This attribute gets the full name of where this location was set. If no full name could be found, this attribute returns `None`. This will throw a `RuntimeError` exception if the location has been invalidated. This attribute is not writable.

> 此属性获取此位置设置的全名。如果找不到全名，此属性将返回`None`。如果位置已失效，则会抛出`RuntimeError`异常。此属性不可写。

```

<!-- -->

```


Variable: **BreakpointLocation.thread_groups**

> 变量：**BreakpointLocation.thread_groups**


:   This attribute gets the thread groups it was set in. It returns a `List` of the thread group ID's. This will throw a `RuntimeError` exception if the location has been invalidated. This attribute is not writable.

> 这个属性获取它被设置的线程组。它返回一个线程组ID的`列表`。如果位置已失效，这将抛出一个`运行时错误`异常。这个属性是不可写的。

---

::: header
Next: [Finish Breakpoints in Python](Finish-Breakpoints-in-Python.html#Finish-Breakpoints-in-Python)]
:::
```
