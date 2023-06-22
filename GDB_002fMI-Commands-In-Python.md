---
description: GDB/MI Commands In Python (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: GDB/MI Commands In Python (Debugging with GDB)
lang: en
resource-type: document
title: GDB/MI Commands In Python (Debugging with GDB)
---
::: header
Next: [Parameters In Python](Parameters-In-Python.html#Parameters-In-Python)]
:::

---

#### 23.3.2.21 [GDB/MI]

It is possible to add [GDB/MI] command is implemented using an instance of the `gdb.MICommand` class, most commonly using a subclass.

Function: **MICommand.__init__** *(name)*

:   The object initializer for `MICommand` registers the new command with [GDB]. This initializer is normally invoked from the subclass' own `__init__` method.

```
`name` command previously defined in Python is allowed, the previous command will be replaced with the new command.
```

```
<!-- -->
```

Function: **MICommand.invoke** *(arguments)*

:   This method is called by [GDB] when the new MI command is invoked.

```
`arguments` itself therefore they do not show up in `arguments`.

If this method raises an exception, then it is turned into a [GDB/MI]](Python-Commands.html#set_005fpython_005fprint_005fstack)).

If this method returns `None`, then the [GDB/MI] command will return a `^done` response with no additional values.

Otherwise, the return value must be a dictionary, which is converted to a [GDB/MI], these strings must comply with the naming rules detailed below. The values of this dictionary are recursively handled as follows:

-   If the value is Python sequence or iterator, it is converted to [GDB/MI] with elements converted recursively.
-   If the value is Python dictionary, it is converted to [GDB/MI] naming rules detailed below. Values are converted recursively.
-   Otherwise, value is first converted to a Python string using `str ()` and then converted to [GDB/MI].

The strings used for `variable` output must follow the following rules; the string must be at least one character long, the first character must be in the set `[a-zA-Z]`, while every subsequent character must be in the set `[-_a-zA-Z0-9]`.
```

An instance of `MICommand` has the following attributes:

Variable: **MICommand.name**

:   A string, the name of this [GDB/MI] command, as was passed to the `__init__` method. This attribute is read-only.

```
<!-- -->
```

Variable: **MICommand.installed**

:   A boolean value indicating if this command is installed ready for a user to call from the command line. Commands are automatically installed when they are instantiated, after which this attribute will be `True`.

```
If later, a new command is created with the same name, then the original command will become uninstalled, and this attribute will be `False`.

This attribute is read-write, setting this attribute to `False` will uninstall the command, removing it from the set of available commands. Setting this attribute to `True` will install the command for use. If there is already a Python command with this name installed, the currently installed command will be uninstalled, and this command installed in its stead.
```

The following code snippet shows how some trivial MI commands can be implemented in Python:

::: smallexample

```bash
class MIEcho(gdb.MICommand):
    """Echo arguments passed to the command."""

    def __init__(self, name, mode):
        self._mode = mode
        super(MIEcho, self).__init__(name)

    def invoke(self, argv):
        if self._mode == 'dict':
            return 
        elif self._mode == 'list':
            return 
        else:
            return 


MIEcho("-echo-dict", "dict")
MIEcho("-echo-list", "list")
MIEcho("-echo-string", "string")
```

:::

The last three lines instantiate the class three times, creating three new [GDB/MI].

Depending on how the Python code is read into [GDB], you may need to import the `gdb` module explicitly.

The following example shows a [GDB] session in which the above commands have been added:

::: smallexample

```bash
(gdb)
-echo-dict abc def ghi
^done,dict=
(gdb)
-echo-list abc def ghi
^done,list=["abc","def","ghi"]
(gdb)
-echo-string abc def ghi
^done,string="abc, def, ghi"
(gdb)
```

:::

Conversely, it is possible to execute [GDB/MI] commands from Python, with the results being a Python object and not a specially-formatted string. This is done with the `gdb.execute_mi` function.

...)*

:   Invoke a [GDB/MI], are passed to the command. Each argument must also be a string.

```
This function returns a Python dictionary whose contents reflect the corresponding [GDB/MI] command's output. Refer to the documentation for these commands for details. Lists are represented as Python lists, and tuples are represented as Python dictionaries.

If the command fails, it will raise a Python exception.
```

Here is how this works using the commands from the example above:

::: smallexample

```bash
(gdb) python print(gdb.execute_mi("-echo-dict", "abc", "def", "ghi"))

(gdb) python print(gdb.execute_mi("-echo-list", "abc", "def", "ghi"))

(gdb) python print(gdb.execute_mi("-echo-string", "abc", "def", "ghi"))

```

:::

---

::: header
Next: [Parameters In Python](Parameters-In-Python.html#Parameters-In-Python)]
:::
