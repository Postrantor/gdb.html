---
description: Finish Breakpoints in Python (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Finish Breakpoints in Python (Debugging with GDB)
lang: en
resource-type: document
title: Finish Breakpoints in Python (Debugging with GDB)
---
::: header
Next: [Lazy Strings In Python](Lazy-Strings-In-Python.html#Lazy-Strings-In-Python)]
:::

---

#### 23.3.2.32 Finish Breakpoints

A finish breakpoint is a temporary breakpoint set at the return address of a frame, based on the `finish` command. `gdb.FinishBreakpoint` extends `gdb.Breakpoint`. The underlying breakpoint will be disabled and deleted when the execution will run out of the breakpoint scope (i.e. `Breakpoint.stop` or `FinishBreakpoint.out_of_scope` triggered). Finish breakpoints are thread specific and must be create with the right thread selected.

)*

:   Create a finish breakpoint at the return address of the `gdb.Frame` object `frame` argument allows the breakpoint to become invisible to the user. See [Breakpoints In Python](Breakpoints-In-Python.html#Breakpoints-In-Python), for further details about this argument.

```
<!-- -->
```

Function: **FinishBreakpoint.out_of_scope** *(self)*

:   In some circumstances (e.g. `longjmp`, C++ exceptions, [GDB] notices such a situation, the `out_of_scope` callback will be triggered.

```
You may want to sub-class `gdb.FinishBreakpoint` and override this method:

::: smallexample
``` smallexample
class MyFinishBreakpoint (gdb.FinishBreakpoint)
    def stop (self):
        print ("normal finish")
        return True
    
    def out_of_scope ():
        print ("abnormal finish")
```

:::

```

```

<!-- -->

```

Variable: **FinishBreakpoint.return_value**

:   When [GDB] is stopped at a finish breakpoint and the frame used to build the `gdb.FinishBreakpoint` object had debug symbols, this attribute will contain a `gdb.Value` object corresponding to the return value of the function. The value will be `None` if the function return type is `void` or if the return value was not computable. This attribute is not writable.

---

::: header
Next: [Lazy Strings In Python](Lazy-Strings-In-Python.html#Lazy-Strings-In-Python)]
:::
```
