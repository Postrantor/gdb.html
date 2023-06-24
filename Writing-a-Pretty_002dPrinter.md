---
tip: translate by openai@2023-06-24 04:53:42
...
---
description: Writing a Pretty-Printer (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Writing a Pretty-Printer (Debugging with GDB)
lang: en
resource-type: document
title: Writing a Pretty-Printer (Debugging with GDB)
---
::: header
Next: [Type Printing API](Type-Printing-API.html#Type-Printing-API)]
:::

---

#### 23.3.2.7 Writing a Pretty-Printer


A pretty-printer consists of two parts: a lookup function to detect if the type is supported, and the printer itself.

> 一个漂亮的打印机由两部分组成：查找函数来检测类型是否受支持，以及打印机本身。


Here is an example showing how a `std::string` printer might be written. See [Pretty Printing API](Pretty-Printing-API.html#Pretty-Printing-API), for details on the API this class must provide.

> 这里有一个示例，展示了如何编写一个`std::string`打印机。有关API必须提供的详细信息，请参阅[Pretty Printing API](Pretty-Printing-API.html#Pretty-Printing-API)。

::: smallexample

```bash
class StdStringPrinter(object):
    "Print a std::string"

    def __init__(self, val):
        self.val = val

    def to_string(self):
        return self.val['_M_dataplus']['_M_p']

    def display_hint(self):
        return 'string'
```

:::


And here is an example showing how a lookup function for the printer example above might be written.

> 这里有一个示例，展示了如何编写上面打印机示例的查找函数。

::: smallexample

```bash
def str_lookup_function(val):
    lookup_tag = val.type.tag
    if lookup_tag is None:
        return None
    regex = re.compile("^std::basic_string<char,.*>$")
    if regex.match(lookup_tag):
        return StdStringPrinter(val)
    return None
```

:::


The example lookup function extracts the value's type, and attempts to match it to a type that it can pretty-print. If it is a type the printer can pretty-print, it will return a printer object. If not, it returns `None`.

> 例如查找函數提取值的類型，並嘗試將其與可以漂亮打印的類型進行匹配。如果它是打印機可以漂亮打印的類型，它將返回一個打印對象。如果不是，它將返回“無”。


We recommend that you put your core pretty-printers into a Python package. If your pretty-printers are for use with a library, we further recommend embedding a version number into the package name. This practice will enable [GDB] to load multiple versions of your pretty-printers at the same time, because they will have different names.

> 我们建议您将核心pretty-printers放入一个Python包中。如果您的pretty-printers用于库，我们进一步建议将版本号嵌入包名中。这种做法将使[GDB]能够同时加载多个版本的pretty-printers，因为它们将具有不同的名称。


You should write auto-loaded code (see [Python Auto-loading](Python-Auto_002dloading.html#Python-Auto_002dloading)) such that it can be evaluated multiple times without changing its meaning. An ideal auto-load file will consist solely of `import` s of your printer modules, followed by a call to a register pretty-printers with the current objfile.

> 你应该编写自动加载的代码（参见[Python 自动加载](Python-Auto_002dloading.html#Python-Auto_002dloading))，以便可以多次评估而不改变其意义。理想的自动加载文件将仅由您的打印机模块的`import`组成，然后调用当前objfile的注册pretty-printers。


Taken as a whole, this approach will scale nicely to multiple inferiors, each potentially using a different library version. Embedding a version number in the Python package name will ensure that [GDB] will find the correct printers for the specific version of the library used by each inferior.

> 总体来看，这种方法可以很好地扩展到多个次要程序，每个次要程序可能使用不同的库版本。在Python包名称中嵌入版本号将确保[GDB]可以为每个次要程序使用的特定库版本找到正确的打印机。


To continue the `std::string` example (see [Pretty Printing API](Pretty-Printing-API.html#Pretty-Printing-API)), this code might appear in `gdb.libstdcxx.v6`:

> 为了继续`std::string`示例(参见[Pretty Printing API](Pretty-Printing-API.html#Pretty-Printing-API))，这段代码可能出现在`gdb.libstdcxx.v6`中：

::: smallexample

```bash
def register_printers(objfile):
    objfile.pretty_printers.append(str_lookup_function)
```

:::

And then the corresponding contents of the auto-load file would be:

::: smallexample

```bash
import gdb.libstdcxx.v6
gdb.libstdcxx.v6.register_printers(gdb.current_objfile())
```

:::


The previous example illustrates a basic pretty-printer. There are a few things that can be improved on. The printer doesn't have a name, making it hard to identify in a list of installed printers. The lookup function has a name, but lookup functions can have arbitrary, even identical, names.

> 上一个例子说明了一个基本的漂亮的打印机。有几件事可以改进。打印机没有名字，在已安装打印机的列表中很难识别。查找函数有名字，但查找函数可以有任意的，甚至相同的名字。


Second, the printer only handles one type, whereas a library typically has several types. One could install a lookup function for each desired type in the library, but one could also have a single lookup function recognize several types. The latter is the conventional way this is handled. If a pretty-printer can handle multiple data types, then its *subprinters* are the printers for the individual data types.

> 第二，打印机只处理一种类型，而图书馆通常有几种类型。可以为图书馆中的每种需要的类型安装查找功能，也可以用单个查找功能识别多种类型。后者是常规处理方法。如果格式化打印机可以处理多种数据类型，那么它的*子打印机*就是各个数据类型的打印机。


The `gdb.printing` module provides a formal way of solving these problems (see [gdb.printing](gdb_002eprinting.html#gdb_002eprinting)). Here is another example that handles multiple types.

> 模块`gdb.printing`提供了一种正式的方式来解决这些问题（参见[gdb.printing](gdb_002eprinting.html#gdb_002eprinting)）。这里有另一个处理多种类型的示例。

These are the types we are going to pretty-print:

::: smallexample

```bash
struct foo ;
struct bar ;
```

:::

Here are the printers:

::: smallexample

```bash
class fooPrinter:
    """Print a foo object."""

    def __init__(self, val):
        self.val = val

    def to_string(self):
        return ("a=<" + str(self.val["a"]) +
                "> b=<" + str(self.val["b"]) + ">")

class barPrinter:
    """Print a bar object."""

    def __init__(self, val):
        self.val = val

    def to_string(self):
        return ("x=<" + str(self.val["x"]) +
                "> y=<" + str(self.val["y"]) + ">")
```

:::


This example doesn't need a lookup function, that is handled by the `gdb.printing` module. Instead a function is provided to build up the object that handles the lookup.

> 这个例子不需要查找函数，这是由`gdb.printing`模块处理的。相反，提供了一个函数来构建处理查找的对象。

::: smallexample

```bash
import gdb.printing

def build_pretty_printer():
    pp = gdb.printing.RegexpCollectionPrettyPrinter(
        "my_library")
    pp.add_printer('foo', '^foo$', fooPrinter)
    pp.add_printer('bar', '^bar$', barPrinter)
    return pp
```

:::

And here is the autoload support:

::: smallexample

```bash
import gdb.printing
import my_library
gdb.printing.register_pretty_printer(
    gdb.current_objfile(),
    my_library.build_pretty_printer())
```

:::

Finally, when this printer is loaded into [GDB]':

::: smallexample

```bash
(gdb) info pretty-printer
my_library.so:
  my_library
    foo
    bar
```

:::

---

::: header
Next: [Type Printing API](Type-Printing-API.html#Type-Printing-API)]
:::
