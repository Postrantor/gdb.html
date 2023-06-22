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

A breakpoint can be created using one of the two forms of the `gdb.Breakpoint` constructor. The first one accepts a string like one would pass to the `break` (see [Setting Breakpoints](Set-Breaks.html#Set-Breaks)) and `watch` (see [Setting Watchpoints](Set-Watchpoints.html#Set-Watchpoints)) commands, and can be used to create both breakpoints and watchpoints. The second accepts separate Python arguments similar to [Explicit Locations](Explicit-Locations.html#Explicit-Locations), and can only be used to create breakpoints.

)*

:   Create a new breakpoint according to `spec`, which is a string naming the location of a breakpoint, or an expression that defines a watchpoint. The string should describe a location in a format recognized by the `break` command (see [Setting Breakpoints](Set-Breaks.html#Set-Breaks)) or, in the case of a watchpoint, by the `watch` command (see [Setting Watchpoints](Set-Watchpoints.html#Set-Watchpoints)).

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

```
`internal` have the same usage as explained previously.
```

The available types are represented by constants defined in the `gdb` module:

`gdb.BP_BREAKPOINT`

Normal code breakpoint.

`gdb.BP_HARDWARE_BREAKPOINT`

Hardware assisted code breakpoint.

`gdb.BP_WATCHPOINT`

Watchpoint breakpoint.

`gdb.BP_HARDWARE_WATCHPOINT`

Hardware assisted watchpoint.

`gdb.BP_READ_WATCHPOINT`

Hardware assisted read watchpoint.

`gdb.BP_ACCESS_WATCHPOINT`

Hardware assisted access watchpoint.

`gdb.BP_CATCHPOINT`

Catchpoint. Currently, this type can't be used when creating `gdb.Breakpoint` objects, but will be present in `gdb.Breakpoint` objects reported from `gdb.BreakpointEvent` s (see [Events In Python](Events-In-Python.html#Events-In-Python)).

The available watchpoint types are represented by constants defined in the `gdb` module:

`gdb.WP_READ`

Read only watchpoint.

`gdb.WP_WRITE`

Write only watchpoint.

`gdb.WP_ACCESS`

Read/Write watchpoint.

Function: **Breakpoint.stop** *(self)*

:   The `gdb.Breakpoint` class can be sub-classed and, in particular, you may choose to implement the `stop` method. If this method is defined in a sub-class of `gdb.Breakpoint`, it will be called when the inferior reaches any location of a breakpoint which instantiates that sub-class. If the method returns `True`, the inferior will be stopped at the location of the breakpoint, otherwise the inferior will continue.

```
If there are multiple breakpoints at the same location with a `stop` method, each one will be called regardless of the return status of the previous. This ensures that all `stop` methods have a chance to execute at that location. In this scenario if one of the methods returns `True` but the others return `False`, the inferior will still be stopped.

You should not alter the execution state of the inferior (i.e., step, next, etc.), alter the current frame context (i.e., change the current active frame), or alter, add or delete any breakpoint. As a general rule, you should not alter any data within [GDB] or the inferior at this time.

Example `stop` implementation:

::: smallexample
``` smallexample
class MyBreakpoint (gdb.Breakpoint):
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

:   Return `True` if this `Breakpoint` object is valid, `False` otherwise. A `Breakpoint` object can become invalid if the user deletes the breakpoint. In this case, the object still exists, but the underlying breakpoint does not. In the cases of watchpoint scope, the watchpoint remains valid even if execution of the inferior leaves the scope of that watchpoint.

```

<!-- -->

```

Function: **Breakpoint.delete** *()*

:   Permanently deletes the [GDB] breakpoint. This also invalidates the Python `Breakpoint` object. Any further access to this object's attributes or methods will raise an error.

```

<!-- -->

```

Variable: **Breakpoint.enabled**

:   This attribute is `True` if the breakpoint is enabled, and `False` otherwise. This attribute is writable. You can use it to enable or disable the breakpoint.

```

<!-- -->

```

Variable: **Breakpoint.silent**

:   This attribute is `True` if the breakpoint is silent, and `False` otherwise. This attribute is writable.

```

Note that a breakpoint can also be silent if it has commands and the first command is `silent`. This is not reported by the `silent` attribute.

```

```

<!-- -->

```

Variable: **Breakpoint.pending**

:   This attribute is `True` if the breakpoint is pending, and `False` otherwise. See [Set Breaks](Set-Breaks.html#Set-Breaks). This attribute is read-only.



Variable: **Breakpoint.thread**

:   If the breakpoint is thread-specific, this attribute holds the thread's global id. If the breakpoint is not thread-specific, this attribute is `None`. This attribute is writable.

```

<!-- -->

```

Variable: **Breakpoint.task**

:   If the breakpoint is Ada task-specific, this attribute holds the Ada task id. If the breakpoint is not task-specific (or the underlying language is not Ada), this attribute is `None`. This attribute is writable.

```

<!-- -->

```

Variable: **Breakpoint.ignore_count**

:   This attribute holds the ignore count for the breakpoint, an integer. This attribute is writable.

```

<!-- -->

```

Variable: **Breakpoint.number**

:   This attribute holds the breakpoint's number --- the identifier used by the user to manipulate the breakpoint. This attribute is not writable.

```

<!-- -->

```

Variable: **Breakpoint.type**

:   This attribute holds the breakpoint's type --- the identifier used to determine the actual breakpoint type or use-case. This attribute is not writable.

```

<!-- -->

```

Variable: **Breakpoint.visible**

:   This attribute tells whether the breakpoint is visible to the user when set, or when the '`info breakpoints`' command is run. This attribute is not writable.

```

<!-- -->

```

Variable: **Breakpoint.temporary**

:   This attribute indicates whether the breakpoint was created as a temporary breakpoint. Temporary breakpoints are automatically deleted after that breakpoint has been hit. Access to this attribute, and all other attributes and functions other than the `is_valid` function, will result in an error after the breakpoint has been hit (as it has been automatically deleted). This attribute is not writable.

```

<!-- -->

```

Variable: **Breakpoint.hit_count**

:   This attribute holds the hit count for the breakpoint, an integer. This attribute is writable, but currently it can only be set to zero.

```

<!-- -->

```

Variable: **Breakpoint.location**

:   This attribute holds the location of the breakpoint, as specified by the user. It is a string. If the breakpoint does not have a location (that is, it is a watchpoint) the attribute's value is `None`. This attribute is not writable.

```

<!-- -->

```

Variable: **Breakpoint.locations**

:   Get the most current list of breakpoint locations that are inserted for this breakpoint, with elements of type `gdb.BreakpointLocation` (described below). This functionality matches that of the `info breakpoint` command (see [Set Breaks](Set-Breaks.html#Set-Breaks)), in that it only retrieves the most current list of locations, thus the list itself when returned is not updated behind the scenes. This attribute is not writable.

```

<!-- -->

```

Variable: **Breakpoint.expression**

:   This attribute holds a breakpoint expression, as specified by the user. It is a string. If the breakpoint does not have an expression (the breakpoint is not a watchpoint) the attribute's value is `None`. This attribute is not writable.

```

<!-- -->

```

Variable: **Breakpoint.condition**

:   This attribute holds the condition of the breakpoint, as specified by the user. It is a string. If there is no condition, this attribute's value is `None`. This attribute is writable.

```

<!-- -->

```

Variable: **Breakpoint.commands**

:   This attribute holds the commands attached to the breakpoint. If there are commands, this attribute's value is a string holding all the commands, separated by newlines. If there are no commands, this attribute is `None`. This attribute is writable.



#### Breakpoint Locations 

A breakpoint location is one of the actual places where a breakpoint has been set, represented in the Python API by the `gdb.BreakpointLocation` type. This type is never instantiated by the user directly, but is retrieved from `Breakpoint.locations` which returns a list of breakpoint locations where it is currently set. Breakpoint locations can become invalid if new symbol files are loaded or dynamically loaded libraries are closed. Accessing the attributes of an invalidated breakpoint location will throw a `RuntimeError` exception. Access the `Breakpoint.locations` attribute again to retrieve the new and valid breakpoints location list.

Variable: **BreakpointLocation.source**

:   This attribute returns the source file path and line number where this location was set. The type of the attribute is a tuple of `string`. If the breakpoint location doesn't have a source location, it returns None, which is the case for watchpoints and catchpoints. This will throw a `RuntimeError` exception if the location has been invalidated. This attribute is not writable.

```

<!-- -->

```

Variable: **BreakpointLocation.address**

:   This attribute returns the address where this location was set. This attribute is of type long. This will throw a `RuntimeError` exception if the location has been invalidated. This attribute is not writable.

```

<!-- -->

```

Variable: **BreakpointLocation.enabled**

:   This attribute holds the value for whether or not this location is enabled. This attribute is writable (boolean). This will throw a `RuntimeError` exception if the location has been invalidated.

```

<!-- -->

```

Variable: **BreakpointLocation.owner**

:   This attribute holds a reference to the `gdb.Breakpoint` owner object, from which this `gdb.BreakpointLocation` was retrieved from. This will throw a `RuntimeError` exception if the location has been invalidated. This attribute is not writable.

```

<!-- -->

```

Variable: **BreakpointLocation.function**

:   This attribute gets the name of the function where this location was set. If no function could be found this attribute returns `None`. This will throw a `RuntimeError` exception if the location has been invalidated. This attribute is not writable.

```

<!-- -->

```

Variable: **BreakpointLocation.fullname**

:   This attribute gets the full name of where this location was set. If no full name could be found, this attribute returns `None`. This will throw a `RuntimeError` exception if the location has been invalidated. This attribute is not writable.

```

<!-- -->

```

Variable: **BreakpointLocation.thread_groups**

:   This attribute gets the thread groups it was set in. It returns a `List` of the thread group ID's. This will throw a `RuntimeError` exception if the location has been invalidated. This attribute is not writable.

---

::: header
Next: [Finish Breakpoints in Python](Finish-Breakpoints-in-Python.html#Finish-Breakpoints-in-Python)]
:::
```
