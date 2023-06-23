---
tip: translate by openai@2023-06-23 15:54:22
...
---
description: Xmethods In Python (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Xmethods In Python (Debugging with GDB)
lang: en
resource-type: document
title: Xmethods In Python (Debugging with GDB)
----------------------------------------------

::: header
Next: [Xmethod API](Xmethod-API.html#Xmethod-API)]
:::

---

#### 23.3.2.13 Xmethods In Python

*Xmethods* are additional methods or replacements for existing methods of a C++ class. This feature is useful for those cases where a method defined in C++ source code could be inlined or optimized out by the compiler, making it unavailable to [GDB] will then invoke the xmethod, instead of the C++ method, to evaluate expressions. One can also use xmethods when debugging with core files. Moreover, when debugging live programs, invoking an xmethod need not involve running the inferior (which can potentially perturb its state). Hence, even if the C++ method is available, it is better to use its replacement xmethod if one is defined.

> *Xmethods* 是 C++ 类的附加方法或替换现有方法。当编译器可能会把 C++ 源代码中定义的方法内联或优化掉，从而使[GDB]无法访问时，这个功能非常有用。然后，GDB 将调用 xmethod 来评估表达式，而不是 C++ 方法。在使用核心文件调试时，也可以使用 xmethods。此外，当调试实时程序时，调用 xmethod 不需要运行下级（这可能会扰乱其状态）。因此，即使 C++ 方法可用，如果定义了替换的 xmethod，也最好使用它。

The xmethods feature in Python is available via the concepts of an *xmethod matcher* and an *xmethod worker*. To implement an xmethod, one has to implement a matcher and a corresponding worker for it (more than one worker can be implemented, each catering to a different overloaded instance of the method). Internally, [GDB] uses the overall winner to invoke the method. If the winning xmethod worker is the overall winner, then the corresponding xmethod is invoked via the `__call__` method of the worker object.

> Python 中的 xmethods 功能可通过 *xmethod matcher* 和 *xmethod worker* 的概念来实现。要实现 xmethod，必须为其实现一个匹配器和相应的工作者（可实现多个工作者，每个工作者都适用于方法的不同重载实例）。内部，[GDB]使用总体获胜者来调用该方法。如果获胜的 xmethod worker 是总体获胜者，则通过工作者对象的 `__call__` 方法调用相应的 xmethod。

If one wants to implement an xmethod as a replacement for an existing C++ method, then they have to implement an equivalent xmethod which has exactly the same name and takes arguments of exactly the same type as the C++ method. If the user wants to invoke the C++ method even though a replacement xmethod is available for that method, then they can disable the xmethod.

> 如果想要实现一个 x 方法来替换现有的 C++ 方法，那么他们必须实现一个与 C++ 方法完全相同的名字和参数类型的 x 方法。如果用户想要调用 C++ 方法，即使有一个替代的 x 方法可用，那么他们可以禁用 x 方法。

See [Xmethod API](Xmethod-API.html#Xmethod-API), for API to implement xmethods in Python. See [Writing an Xmethod](Writing-an-Xmethod.html#Writing-an-Xmethod), for implementing xmethods in Python.

> 请参阅 [Xmethod API](Xmethod-API.html#Xmethod-API)，以了解如何在 Python 中实现 xmethods。另请参阅 [Writing an Xmethod](Writing-an-Xmethod.html#Writing-an-Xmethod)，以了解如何在 Python 中实现 xmethods。

---

::: header
Next: [Xmethod API](Xmethod-API.html#Xmethod-API)]
:::
