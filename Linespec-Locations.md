---
tip: translate by openai@2023-06-23 23:52:23
...
---
description: Linespec Locations (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Linespec Locations (Debugging with GDB)
lang: en
resource-type: document
title: Linespec Locations (Debugging with GDB)
---
::: header
Next: [Explicit Locations](Explicit-Locations.html#Explicit-Locations)]
:::

---

#### 9.2.1 Linespec Locations


A *linespec* is a colon-separated list of source location parameters such as file name, function name, etc. Here are all the different ways of specifying a linespec:

> 一个*linespec*是一个由冒号分隔的源位置参数列表，例如文件名、函数名等。以下是指定linespec的不同方式：

`linenum`

:   Specifies the line number `linenum` of the current source file.

`-offset`
`+offset`

:   Specifies the line `offset` lines up or down from the first linespec.

`filename:linenum`

:   Specifies the line `linenum`.

`function`


:   Specifies the line that begins the body of the function `function`. For example, in C, this is the line with the open brace.

> 指定函数体开始的行，例如，在C中，这是带有开括号的行。

```
By default, in C++ and Ada, `function` in all scopes. For C++, this means in all namespaces and classes. For Ada, this means in all packages.

For example, assuming a program with C++ symbols named `A::B::func` and `B::func`, both commands [break func] set a breakpoint on both symbols.

Commands that accept a linespec let you override this with the `-qualified` option. For example, [break [-qualified] sets a breakpoint on a free-function named `func` ignoring any C++ class methods and namespace functions called `func`.

See [Explicit Locations](Explicit-Locations.html#Explicit-Locations).
```

`function:label`

:   Specifies the line where `label`.

`filename:function`


:   Specifies the line that begins the body of the function `function`. You only need the file name with a function name to avoid ambiguity when there are identically named functions in different source files.

> 指定开始函数体的行，函数名称为`function`。当不同源文件中存在相同名称的函数时，只需要文件名和函数名来避免歧义。

`label`


:   Specifies the line at which the label named `label` will not search for a label.

> 指定名为`label`的标签不会搜索的行。

```

```

`-pstap|-probe-stap [objfile:[provider:]]name`


:   The [GNU]/Linux tool `SystemTap` provides a way for applications to embed static probes. See [Static Probe Points](Static-Probe-Points.html#Static-Probe-Points), for more information on finding and using static probes. This form of linespec specifies the location of such a static probe.

> 在GNU/Linux系统中，`SystemTap`工具可以为应用程序提供嵌入静态探针的方法。有关查找和使用静态探针的更多信息，请参见[静态探针点](Static-Probe-Points.html#Static-Probe-Points)。此种形式的linespec指定了这种静态探针的位置。

```
If `objfile` will insert a breakpoint at each one of those probes.
```

---

::: header
Next: [Explicit Locations](Explicit-Locations.html#Explicit-Locations)]
:::
