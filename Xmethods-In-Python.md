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

The xmethods feature in Python is available via the concepts of an *xmethod matcher* and an *xmethod worker*. To implement an xmethod, one has to implement a matcher and a corresponding worker for it (more than one worker can be implemented, each catering to a different overloaded instance of the method). Internally, [GDB] uses the overall winner to invoke the method. If the winning xmethod worker is the overall winner, then the corresponding xmethod is invoked via the `__call__` method of the worker object.

If one wants to implement an xmethod as a replacement for an existing C++ method, then they have to implement an equivalent xmethod which has exactly the same name and takes arguments of exactly the same type as the C++ method. If the user wants to invoke the C++ method even though a replacement xmethod is available for that method, then they can disable the xmethod.

See [Xmethod API](Xmethod-API.html#Xmethod-API), for API to implement xmethods in Python. See [Writing an Xmethod](Writing-an-Xmethod.html#Writing-an-Xmethod), for implementing xmethods in Python.

---

::: header
Next: [Xmethod API](Xmethod-API.html#Xmethod-API)]
:::
