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

Here is an example showing how a `std::string` printer might be written. See [Pretty Printing API](Pretty-Printing-API.html#Pretty-Printing-API), for details on the API this class must provide.

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

We recommend that you put your core pretty-printers into a Python package. If your pretty-printers are for use with a library, we further recommend embedding a version number into the package name. This practice will enable [GDB] to load multiple versions of your pretty-printers at the same time, because they will have different names.

You should write auto-loaded code (see [Python Auto-loading](Python-Auto_002dloading.html#Python-Auto_002dloading)) such that it can be evaluated multiple times without changing its meaning. An ideal auto-load file will consist solely of `import` s of your printer modules, followed by a call to a register pretty-printers with the current objfile.

Taken as a whole, this approach will scale nicely to multiple inferiors, each potentially using a different library version. Embedding a version number in the Python package name will ensure that [GDB] will find the correct printers for the specific version of the library used by each inferior.

To continue the `std::string` example (see [Pretty Printing API](Pretty-Printing-API.html#Pretty-Printing-API)), this code might appear in `gdb.libstdcxx.v6`:

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

Second, the printer only handles one type, whereas a library typically has several types. One could install a lookup function for each desired type in the library, but one could also have a single lookup function recognize several types. The latter is the conventional way this is handled. If a pretty-printer can handle multiple data types, then its *subprinters* are the printers for the individual data types.

The `gdb.printing` module provides a formal way of solving these problems (see [gdb.printing](gdb_002eprinting.html#gdb_002eprinting)). Here is another example that handles multiple types.

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
