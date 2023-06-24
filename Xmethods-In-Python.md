---
tip: translate by openai@2023-06-24 04:59:23
...
---
description: Xmethods In Python (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Xmethods In Python (Debugging with GDB)
lang: en
resource-type: document
title: Xmethods In Python (Debugging with GDB)
---
::: header
Next: [Xmethod API](Xmethod-API.html#Xmethod-API)]
:::

---

#### 23.3.2.13 Xmethods In Python


*Xmethods* are additional methods or replacements for existing methods of a C++ class. This feature is useful for those cases where a method defined in C++ source code could be inlined or optimized out by the compiler, making it unavailable to [GDB] will then invoke the xmethod, instead of the C++ method, to evaluate expressions. One can also use xmethods when debugging with core files. Moreover, when debugging live programs, invoking an xmethod need not involve running the inferior (which can potentially perturb its state). Hence, even if the C++ method is available, it is better to use its replacement xmethod if one is defined.

> *Xmethods*是C++类的附加方法或替换现有方法。当编译器可能会对C++源代码中定义的方法进行内联或优化时，这个功能就非常有用，因此[GDB]将调用xmethod来评估表达式，而不是C++方法。当使用核心文件调试时，也可以使用xmethods。此外，当调试实时程序时，调用xmethod不需要运行次级（可能会扰乱其状态）。因此，即使C++方法可用，如果定义了替代的xmethod，最好使用它。


The xmethods feature in Python is available via the concepts of an *xmethod matcher* and an *xmethod worker*. To implement an xmethod, one has to implement a matcher and a corresponding worker for it (more than one worker can be implemented, each catering to a different overloaded instance of the method). Internally, [GDB] uses the overall winner to invoke the method. If the winning xmethod worker is the overall winner, then the corresponding xmethod is invoked via the `__call__` method of the worker object.

> Python中的xmethods功能可以通过一个*xmethod matcher*和一个*xmethod worker*来实现。要实现一个xmethod，需要为它实现一个matcher和一个相应的worker（可以实现多个worker，每个worker都服务于该方法的不同重载实例）。在内部，[GDB]使用总体获胜者来调用该方法。如果获胜的xmethod worker是总体获胜者，那么就通过worker对象的`__call__`方法来调用相应的xmethod。


If one wants to implement an xmethod as a replacement for an existing C++ method, then they have to implement an equivalent xmethod which has exactly the same name and takes arguments of exactly the same type as the C++ method. If the user wants to invoke the C++ method even though a replacement xmethod is available for that method, then they can disable the xmethod.

> 如果一个人想用一个xmethod来替换现有的C++方法，那么他们必须实现一个等价的xmethod，它具有与C++方法完全相同的名称和参数类型。如果用户想要调用C++方法，即使有一个可用的替代xmethod，他们也可以禁用xmethod。


See [Xmethod API](Xmethod-API.html#Xmethod-API), for API to implement xmethods in Python. See [Writing an Xmethod](Writing-an-Xmethod.html#Writing-an-Xmethod), for implementing xmethods in Python.

> 请参阅[Xmethod API](Xmethod-API.html#Xmethod-API)，了解如何在Python中实现Xmethods。参阅[Writing an Xmethod](Writing-an-Xmethod.html#Writing-an-Xmethod)，了解如何在Python中实现Xmethods。

---

::: header
Next: [Xmethod API](Xmethod-API.html#Xmethod-API)]
:::
