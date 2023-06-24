---
tip: translate by openai@2023-06-24 01:30:19
...
---
description: Progspaces In Guile (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Progspaces In Guile (Debugging with GDB)
lang: en
resource-type: document
title: Progspaces In Guile (Debugging with GDB)
---
::: header
Next: [Objfiles In Guile](Objfiles-In-Guile.html#Objfiles-In-Guile)]
:::

---

#### 23.4.3.13 Program Spaces In Guile


A program space, or *progspace*, represents a symbolic view of an address space. It consists of all of the objfiles of the program. See [Objfiles In Guile](Objfiles-In-Guile.html#Objfiles-In-Guile). See [program spaces](Inferiors-Connections-and-Programs.html#Inferiors-Connections-and-Programs), for more details about program spaces.

> 一个程序空间，或者*progspace*，代表一个地址空间的象征性视图。它包括程序的所有objfiles。参见[Guile中的Objfiles](Objfiles-In-Guile.html#Objfiles-In-Guile)。有关程序空间的更多详细信息，请参阅[程序空间](Inferiors-Connections-and-Programs.html#Inferiors-Connections-and-Programs)。


Each progspace is represented by an instance of the `<gdb:progspace>` smob. See [GDB Scheme Data Types](GDB-Scheme-Data-Types.html#GDB-Scheme-Data-Types).

> 每个progspace都由`<gdb:progspace>` smob的一个实例表示。请参阅[GDB Scheme Data Types](GDB-Scheme-Data-Types.html#GDB-Scheme-Data-Types)。


The following progspace-related functions are available in the `(gdb)` module:

> 以下与Progspace相关的功能可在`(gdb)`模块中使用：

Scheme Procedure: **progspace?** *object*


:   Return `#t` if `object` is a `<gdb:progspace>` object. Otherwise return `#f`.

> 如果对象是一个<gdb:progspace>对象，则返回#t。否则返回#f。

```
<!-- -->
```

Scheme Procedure: **progspace-valid?** *progspace*

:   Return `#t` if `progspace` any longer.

```
<!-- -->
```

Scheme Procedure: **current-progspace**


:   This function returns the program space of the currently selected inferior. There is always a current progspace, this never returns `#f`. See [Inferiors Connections and Programs](Inferiors-Connections-and-Programs.html#Inferiors-Connections-and-Programs).

> 这个函数返回当前选定的次级程序的程序空间。总是有一个当前的progspace，它永远不会返回“#f”。请参见[次级连接和程序](Inferiors-Connections-and-Programs.html#Inferiors-Connections-and-Programs)。

```
<!-- -->
```

Scheme Procedure: **progspaces**

:   Return a list of all the progspaces currently known to [GDB].

```
<!-- -->
```

Scheme Procedure: **progspace-filename** *progspace*


:   Return the absolute file name of `progspace` is started without a program to debug.

> 返回progspace启动时没有程序调试的绝对文件名。

```
A `gdb:invalid-object-error` exception is thrown if `progspace` is invalid.
```

```
<!-- -->
```

Scheme Procedure: **progspace-objfiles** *progspace*


:   Return the list of objfiles of `progspace`. The order of objfiles in the result is arbitrary. Each element is an object of type `<gdb:objfile>`. See [Objfiles In Guile](Objfiles-In-Guile.html#Objfiles-In-Guile).

> 返回`progspace`的objfiles列表。结果中objfiles的顺序是任意的。每个元素都是类型为`<gdb:objfile>`的对象。请参见[Guile中的Objfiles](Objfiles-In-Guile.html#Objfiles-In-Guile)。

```
A `gdb:invalid-object-error` exception is thrown if `progspace` is invalid.
```

```
<!-- -->
```

Scheme Procedure: **progspace-pretty-printers** *progspace*


:   Return the list of pretty-printers of `progspace`. Each element is an object of type `<gdb:pretty-printer>`. See [Guile Pretty Printing API](Guile-Pretty-Printing-API.html#Guile-Pretty-Printing-API), for more information.

> 返回`progspace`的可美化打印机列表。每个元素都是`<gdb:pretty-printer>`类型的对象。有关更多信息，请参阅[Guile Pretty Printing API](Guile-Pretty-Printing-API.html#Guile-Pretty-Printing-API)。

```
<!-- -->
```


Scheme Procedure: **set-progspace-pretty-printers!** *progspace printer-list*

> 设置程序空间格式化打印器！ *progspace printer-list*


:   Set the list of registered `<gdb:pretty-printer>` objects for `progspace`. See [Guile Pretty Printing API](Guile-Pretty-Printing-API.html#Guile-Pretty-Printing-API), for more information.

> 设置为progspace注册的`<gdb:pretty-printer>`对象列表。有关更多信息，请参阅[Guile Pretty Printing API](Guile-Pretty-Printing-API.html#Guile-Pretty-Printing-API)。

---

::: header
Next: [Objfiles In Guile](Objfiles-In-Guile.html#Objfiles-In-Guile)]
:::
