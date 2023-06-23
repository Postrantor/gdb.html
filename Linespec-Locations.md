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

`linenum`

:   Specifies the line number `linenum` of the current source file.

`-offset`
`+offset`

:   Specifies the line `offset` lines up or down from the first linespec.

`filename:linenum`

:   Specifies the line `linenum`.

`function`

:   Specifies the line that begins the body of the function `function`. For example, in C, this is the line with the open brace.

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

`label`

:   Specifies the line at which the label named `label` will not search for a label.

```

```

`-pstap|-probe-stap [objfile:[provider:]]name`

:   The [GNU]/Linux tool `SystemTap` provides a way for applications to embed static probes. See [Static Probe Points](Static-Probe-Points.html#Static-Probe-Points), for more information on finding and using static probes. This form of linespec specifies the location of such a static probe.

```
If `objfile` will insert a breakpoint at each one of those probes.
```

---

::: header
Next: [Explicit Locations](Explicit-Locations.html#Explicit-Locations)]
:::
