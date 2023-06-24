---
tip: translate by openai@2023-06-24 00:38:32
...
---
description: Objfiles In Guile (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Objfiles In Guile (Debugging with GDB)
lang: en
resource-type: document
title: Objfiles In Guile (Debugging with GDB)
---
::: header
Next: [Frames In Guile](Frames-In-Guile.html#Frames-In-Guile)]
:::

---

#### 23.4.3.14 Objfiles In Guile

[GDB] calls these symbol-containing files *objfiles*.

Each objfile is represented as an object of type `<gdb:objfile>`.


The following objfile-related procedures are provided by the `(gdb)` module:

> `(gdb)` 模块提供以下与 objfile 相关的程序：

Scheme Procedure: **objfile?** *object*


:   Return `#t` if `object` is a `<gdb:objfile>` object. Otherwise return `#f`.

> 如果对象是<gdb:objfile>对象，则返回#t。否则返回#f。

```
<!-- -->
```

Scheme Procedure: **objfile-valid?** *objfile*


:   Return `#t` if `objfile` any longer. All other `<gdb:objfile>` procedures will throw an exception if it is invalid at the time the procedure is called.

> 如果`objfile`仍然有效，则返回`#t`。其他所有`<gdb:objfile>`过程都将在调用时如果无效则抛出异常。

```
<!-- -->
```

Scheme Procedure: **objfile-filename** *objfile*


:   Return the file name of `objfile` as a string, with symbolic links resolved.

> 返回`objfile`的文件名作为一个字符串，解析已解析的符号链接。

```
<!-- -->
```

Scheme Procedure: **objfile-progspace** *objfile*


:   Return the `<gdb:progspace>` that this object file lives in. See [Progspaces In Guile](Progspaces-In-Guile.html#Progspaces-In-Guile), for more on progspaces.

> 返回此对象文件所属的<gdb:progspace>。有关progspaces的更多信息，请参阅[Guile中的Progspaces]（Progspaces-In-Guile.html#Progspaces-In-Guile）。

```
<!-- -->
```

Scheme Procedure: **objfile-pretty-printers** *objfile*


:   Return the list of registered `<gdb:pretty-printer>` objects for `objfile`. See [Guile Pretty Printing API](Guile-Pretty-Printing-API.html#Guile-Pretty-Printing-API), for more information.

> 返回为对象文件注册的<gdb:pretty-printer>对象列表。有关更多信息，请参阅Guile Pretty Printing API。

```
<!-- -->
```

Scheme Procedure: **set-objfile-pretty-printers!** *objfile printer-list*


:   Set the list of registered `<gdb:pretty-printer>` objects for `objfile` must be a list of `<gdb:pretty-printer>` objects. See [Guile Pretty Printing API](Guile-Pretty-Printing-API.html#Guile-Pretty-Printing-API), for more information.

> 设置objfile的注册<gdb:pretty-printer>对象列表必须是<gdb:pretty-printer>对象列表。有关更多信息，请参阅[Guile Pretty Printing API](Guile-Pretty-Printing-API.html#Guile-Pretty-Printing-API)。

```
<!-- -->
```

Scheme Procedure: **current-objfile**


:   When auto-loading a Guile script (see [Guile Auto-loading](Guile-Auto_002dloading.html#Guile-Auto_002dloading)), [GDB] sets the "current objfile" to the corresponding objfile. This function returns the current objfile. If there is no current objfile, this function returns `#f`.

> 当自动加载Guile脚本时（参见[Guile Auto-loading](Guile-Auto_002dloading.html#Guile-Auto_002dloading)），[GDB]将“当前objfile”设置为相应的objfile。此函数返回当前objfile。如果没有当前objfile，此函数返回`#f`。

```
<!-- -->
```

Scheme Procedure: **objfiles**

:   Return a list of all the objfiles in the current program space.

---

::: header
Next: [Frames In Guile](Frames-In-Guile.html#Frames-In-Guile)]
:::
