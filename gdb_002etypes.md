---
tip: translate by openai@2023-06-23 21:41:22
...
---
description: gdb.types (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: gdb.types (Debugging with GDB)
lang: en
resource-type: document
title: gdb.types (Debugging with GDB)
---
::: header
Next: [gdb.prompt](gdb_002eprompt.html#gdb_002eprompt)]
:::

---

#### 23.3.4.2 gdb.types


This module provides a collection of utilities for working with `gdb.Type` objects.

> 这个模块提供了一组用于处理`gdb.Type`对象的实用程序。

`get_basic_type (type)`


:   Return `type` with const and volatile qualifiers stripped, and with typedefs and C++ references converted to the underlying type.

> 返回去除常量和易变性限定符、将类型定义和C++引用转换为底层类型的`type`。

```
C++ example:

::: smallexample
``` smallexample
typedef const int const_int;
const_int foo (3);
const_int& foo_ref (foo);
int main () 
```

:::

Then in gdb:

::: smallexample

```bash
(gdb) start
(gdb) python import gdb.types
(gdb) python foo_ref = gdb.parse_and_eval("foo_ref")
(gdb) python print gdb.types.get_basic_type(foo_ref.type)
int
```

:::

```

`has_field (type, field)`

:   Return `True` if `type`.

`make_enum_dict (enum_type)`

:   Return a Python `dictionary` type produced from `enum_type`.

`deep_items (type)`


:   Returns a Python iterator similar to the standard `gdb.Type.iteritems` method, except that the iterator returned by `deep_items` will recursively traverse anonymous struct or union fields. For example:

> 返回一个类似于标准`gdb.Type.iteritems`方法的Python迭代器，不同的是`deep_items`返回的迭代器将递归遍历匿名结构体或联合体字段。例如：

```

::: smallexample

```bash
struct A
{
    int a;
    union {
        int b0;
        int b1;
    };
};
```

:::

Then in [GDB]:

::: smallexample

```bash
(gdb) python import gdb.types
(gdb) python struct_a = gdb.lookup_type("struct A")
(gdb) python print struct_a.keys ()

(gdb) python print [k for k,v in gdb.types.deep_items(struct_a)]

```

:::

```

`get_type_recognizers ()`


:   Return a list of the enabled type recognizers for the current context. This is called by [GDB] during the type-printing process (see [Type Printing API](Type-Printing-API.html#Type-Printing-API)).

> 返回当前上下文中启用的类型识别器列表。[GDB]在类型打印过程中调用此函数（请参阅[类型打印API]（Type-Printing-API.html＃Type-Printing-API））。

`apply_type_recognizers (recognizers, type_obj)`


:   Apply the type recognizers, `recognizers` during the type-printing process (see [Type Printing API](Type-Printing-API.html#Type-Printing-API)).

> 在类型打印过程中应用类型识别器（参见[类型打印 API](Type-Printing-API.html#Type-Printing-API））。

`register_type_printer (locus, printer)`


:   This is a convenience function to register a type printer `printer` argument is either a `gdb.Objfile`, in which case the printer is registered with that objfile; a `gdb.Progspace`, in which case the printer is registered with that progspace; or `None`, in which case the printer is registered globally.

> 这是一个方便的函数来注册一个类型的打印机。'printer'参数可以是一个`gdb.Objfile`，在这种情况下，打印机将与该objfile注册；一个`gdb.Progspace`，在这种情况下，打印机将与该progspace注册；或者`None`，在这种情况下，打印机将全局注册。

`TypePrinter`


:   This is a base class that implements the type printer protocol. Type printers are encouraged, but not required, to derive from this class. It defines a constructor:

> 这是一个实现类型打印协议的基类。鼓励但不强制要求从这个类派生类型打印机。它定义了一个构造函数：

```

Method on TypePrinter: **__init__** *(self, name)*

:   Initialize the type printer with the given name. The new printer starts in the enabled state.

```

---

::: header
Next: [gdb.prompt](gdb_002eprompt.html#gdb_002eprompt)]
:::
```
