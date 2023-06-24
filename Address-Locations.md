---
tip: translate by openai@2023-06-23 17:04:58
...
---
description: Address Locations (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Address Locations (Debugging with GDB)
lang: en
resource-type: document
title: Address Locations (Debugging with GDB)
---
::: header
Previous: [Explicit Locations](Explicit-Locations.html#Explicit-Locations)]
:::

---

#### 9.2.3 Address Locations


*Address locations* indicate a specific program address. They have the generalized form \*`address`.

> *地址位置*表示特定程序地址。它们具有通用的形式\*`地址`。


For line-oriented commands, such as `list` and `edit`, this specifies a source line that contains `address`. For `break` and other breakpoint-oriented commands, this can be used to set breakpoints in parts of your program which do not have debugging information or source files.

> 对于基于行的命令，例如`list`和`edit`，这会指定一个包含`address`的源行。对于`break`和其他断点定位的命令，可以用它来在程序的没有调试信息或源文件的部分设置断点。

Here `address`:

`expression`


:   Any expression valid in the current working language.

> 任何在当前工作语言中有效的表达式。

`funcaddr`


:   An address of a function or procedure derived from its name. In C, C++, Objective-C, Fortran, minimal, and assembly, this is simply the function's name `function` (and actually a special case of a valid expression). In Pascal and Modula-2, this is `&function`. In Ada, this is `function'Address` (although the Pascal form also works).

> 函数或过程的地址从其名称派生。在C、C++、Objective-C、Fortran、minimal和assembly中，这只是函数的名称`function`（实际上是有效表达式的特殊情况）。在Pascal和Modula-2中，这是`&function`。在Ada中，这是`function'Address`（尽管Pascal形式也有效）。

```
This form specifies the address of the function's first instruction, before the stack frame and arguments have been set up.
```

`'filename':funcaddr`


:   Like `funcaddr` above, but also specifies the name of the source file explicitly. This is useful if the name of the function does not specify the function unambiguously, e.g., if there are several functions with identical names in different source files.

> 就像上面的`funcaddr`一样，但也明确指定源文件的名称。如果函数名不能明确指定函数，例如在不同的源文件中有相同的函数名，则这是有用的。
