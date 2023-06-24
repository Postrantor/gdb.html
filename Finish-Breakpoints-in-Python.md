---
tip: translate by openai@2023-06-23 21:12:05
...
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

> 完成断点是基于`finish`命令在帧的返回地址处设置的临时断点。`gdb.FinishBreakpoint`扩展了`gdb.Breakpoint`。当执行跑出断点范围（即触发`Breakpoint.stop`或`FinishBreakpoint.out_of_scope`）时，底层断点将被禁用和删除。完成断点是特定于线程的，必须使用正确的线程创建。

)*


:   Create a finish breakpoint at the return address of the `gdb.Frame` object `frame` argument allows the breakpoint to become invisible to the user. See [Breakpoints In Python](Breakpoints-In-Python.html#Breakpoints-In-Python), for further details about this argument.

> 在`gdb.Frame`对象`frame`参数的返回地址处创建一个完成断点，这允许断点对用户不可见。有关此参数的更多详细信息，请参阅[Python中的断点](Breakpoints-In-Python.html#Breakpoints-In-Python)。

```
<!-- -->
```

Function: **FinishBreakpoint.out_of_scope** *(self)*


:   In some circumstances (e.g. `longjmp`, C++ exceptions, [GDB] notices such a situation, the `out_of_scope` callback will be triggered.

> 在某些情况下（例如`longjmp`，C++异常，[GDB]注意到这种情况），`out_of_scope`回调将被触发。

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

> 当[GDB]停在结束断点处，并且用于构建`gdb.FinishBreakpoint`对象的帧具有调试符号时，此属性将包含一个与函数返回值对应的`gdb.Value`对象。如果函数返回类型为`void`或者返回值不可计算，则该值为`None`。此属性不可写。

---

::: header
Next: [Lazy Strings In Python](Lazy-Strings-In-Python.html#Lazy-Strings-In-Python)]
:::
```
