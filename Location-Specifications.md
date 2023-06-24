---
tip: translate by openai@2023-06-23 23:55:27
...
---
description: Location Specifications (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Location Specifications (Debugging with GDB)
lang: en
resource-type: document
title: Location Specifications (Debugging with GDB)
---
::: header
Next: [Edit](Edit.html#Edit)]
:::

---

### 9.2 Location Specifications

Several [GDB] recognizes.


When you specify a location, [GDB] needs to find the place in your program, known as *code location*, that corresponds to the given location spec. We call this process of finding actual code locations corresponding to a location spec *location resolution*.

> 当您指定一个位置时，[GDB]需要找到程序中与给定位置规范对应的位置，称为*代码位置*。我们称此过程为找到与位置规范对应的实际代码位置为*位置解析*。


A concrete code location in your program is uniquely identifiable by a set of several attributes: its source line number, the name of its source file, the fully-qualified and prototyped function in which it is defined, and an instruction address. Because each inferior has its own address space, the inferior number is also a necessary part of these attributes.

> 一个程序中的具体代码位置可以由几个属性唯一标识：它的源代码行号、源文件名、定义它的完全限定和原型函数以及指令地址。由于每个次级都有自己的地址空间，所以次级编号也是这些属性中必要的一部分。


By contrast, location specs you type will many times omit some of these attributes. For example, it is customary to specify just the source line number to mean a line in the current source file, or specify just the basename of the file, omitting its directories. In other words, a location spec is usually incomplete, a kind of blueprint, and [GDB] needs to complete the missing attributes by using the implied defaults, and by considering the source code and the debug information available to it. This is what location resolution is about.

> 相反，您输入的位置规范往往会省略其中一些属性。例如，通常只指定源行号以表示当前源文件中的行，或只指定文件的基本名称，而省略其目录。换句话说，位置规范通常是不完整的，是一种蓝图，[GDB]需要通过使用隐含的默认值，并考虑可用的源代码和调试信息来完成缺失的属性。这就是位置解析的本质。


The resolution of an incomplete location spec can produce more than a single code location, if the spec doesn't allow distinguishing between them. Here are some examples of situations that result in a location spec matching multiple code locations in your program:

> 解析不完整的位置规范可能会产生多个代码位置，如果该规范不允许区分它们。以下是一些导致程序中的位置规范匹配多个代码位置的情况的例子：


- The location spec specifies a function name, and there are several functions in the program which have that name. (To distinguish between them, you can specify a fully-qualified and prototyped function name, such as `A::func(int)` instead of just `func`.)

> 指定位置指定了一个函数名，程序中有几个函数都有这个名字。（为了区分它们，你可以指定一个完整的、有原型的函数名，比如 `A::func(int)`，而不只是 `func`。）

- The location spec specifies a source file name, and there are several source files in the program that share the same name, for example several files with the same basename in different subdirectories. (To distinguish between them, specify enough leading directories with the file name.)

> 指定位置规范指定了源文件名称，程序中有几个共享相同名称的源文件，例如，在不同子目录中有几个具有相同基本名称的文件。（为了区分它们，请指定足够的前导目录与文件名称。）

- For a C++ constructor, the [GCC] compiler generates several instances of the function body, used in different cases, but their source-level names are identical.

> 为了C++构造函数，[GCC]编译器生成了几个不同情况下使用的函数体的实例，但它们的源级名称是相同的。

- For a C++ template function, a given line in the function can correspond to any number of instantiations.

> 对于C++模板函数，给定函数中的一行可以对应任意数量的实例化。

- For an inlined function, a given source line can correspond to several actual code locations with that function's inlined code.

> 对于内联函数，给定的源代码行可以对应到几个实际的代码位置，其中包含该函数的内联代码。


Resolution of a location spec can also fail to produce a complete code location, or even fail to produce any code location. Here are some examples of such situations:

> 位置规格的解析也可能无法产生完整的代码位置，甚至无法产生任何代码位置。以下是一些这种情况的示例：


- Some parts of the program lack detailed enough debug info, so the resolved code location lacks some attributes, like source file name and line number, leaving just the instruction address and perhaps also a function name. Such an incomplete code location is only usable in contexts that work with addresses and/or function names. Some commands can only work with complete code locations.

> 部分程序缺乏足够详细的调试信息，因此解析的代码位置缺少一些属性，如源文件名和行号，只留下指令地址和函数名。这种不完整的代码位置仅在处理地址和/或函数名的上下文中可用。某些命令只能使用完整的代码位置。

- The location spec specifies a function name, and there are no functions in the program by that name, or they only exist in a yet-unloaded shared library.

> 指定的位置规范指定了一个函数名，但是程序中没有这个名字的函数，或者它们只存在于尚未加载的共享库中。

- The location spec specifies a source file name, and there are no source files in the program by that name, or they only exist in a yet-unloaded shared library.

> 位置规范指定了一个源文件名称，但程序中没有任何以该名称命名的源文件，或者它们只存在于尚未加载的共享库中。

- The location spec specifies both a source file name and a source line number, and even though there are source files in the program that match the file name, none of those files has the specified line number.

> 指定位置指定了源文件名称和源行号，尽管程序中有符合该文件名称的源文件，但其中没有指定的行号。


Locations may be specified using three different formats: linespec locations, explicit locations, or address locations. The following subsections describe these formats.

> 可以使用三种不同的格式来指定位置：linespec位置、明确的位置或地址位置。下面的小节将描述这些格式。

---


• [Linespec Locations](Linespec-Locations.html#Linespec-Locations):        Linespec locations

> • [Linespec 位置](Linespec-Locations.html#Linespec-Locations):        Linespec 位置

• [Explicit Locations](Explicit-Locations.html#Explicit-Locations):        Explicit locations

> • [明确位置](Explicit-Locations.html#Explicit-Locations):        明确的位置

• [Address Locations](Address-Locations.html#Address-Locations):           Address locations

> • [地址位置](Address-Locations.html#Address-Locations):           地址位置

---

---

::: header
Next: [Edit](Edit.html#Edit)]
:::
