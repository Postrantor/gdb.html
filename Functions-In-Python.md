---
tip: translate by openai@2023-06-23 21:31:28
...
---
description: Functions In Python (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Functions In Python (Debugging with GDB)
lang: en
resource-type: document
title: Functions In Python (Debugging with GDB)
---
::: header
Next: [Progspaces In Python](Progspaces-In-Python.html#Progspaces-In-Python)]
:::

---

#### 23.3.2.23 Writing new convenience functions


You can implement new convenience functions (see [Convenience Vars](Convenience-Vars.html#Convenience-Vars)) in Python. A convenience function is an instance of a subclass of the class `gdb.Function`.

> 你可以在Python中实现新的便捷功能（参见[Convenience Vars](Convenience-Vars.html#Convenience-Vars)）。便捷函数是`gdb.Function`类的子类的一个实例。

Function: **Function.__init__** *(name)*

:   The initializer for `Function` registers the new function with [GDB].

```
The documentation for the new function is taken from the documentation string for the new class.
```

```
<!-- -->
```

Function: **Function.invoke** *(\*args)*


:   When a convenience function is evaluated, its arguments are converted to instances of `gdb.Value`, and then the function's `invoke` method is called. Note that [GDB] does not predetermine the arity of convenience functions. Instead, all available arguments are passed to `invoke`, following the standard Python calling convention. In particular, a convenience function can have default values for parameters without ill effect.

> 当一个便利函数被评估时，它的参数会被转换为`gdb.Value`的实例，然后调用该函数的`invoke`方法。请注意，[GDB]不会预先确定便利函数的参数个数。相反，所有可用的参数都会按照标准Python调用约定传递给`invoke`。特别是，便利函数可以有默认参数值而不会有不良影响。

```
The return value of this method is used as its value in the enclosing expression. If an ordinary Python value is returned, it is converted to a `gdb.Value` following the usual rules.
```


The following code snippet shows how a trivial convenience function can be implemented in Python:

> 以下代码片段展示了如何在Python中实现一个琐碎的便利函数：

::: smallexample

```bash
class Greet (gdb.Function):
  """Return string to greet someone.
Takes a name as argument."""

  def __init__ (self):
    super (Greet, self).__init__ ("greet")

  def invoke (self, name):
    return "Hello, %s!" % name.string ()

Greet ()
```

:::


The last line instantiates the class, and is necessary to trigger the registration of the function with [GDB], you may need to import the `gdb` module explicitly.

> 最后一行实例化该类，并且需要触发函数在[GDB]中的注册，可能需要显式地导入`gdb`模块。

Now you can use the function in an expression:

::: smallexample

```bash
(gdb) print $greet("Bob")
$1 = "Hello, Bob!"
```

:::

---

::: header
Next: [Progspaces In Python](Progspaces-In-Python.html#Progspaces-In-Python)]
:::
