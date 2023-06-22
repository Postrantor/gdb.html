---
description: Pretty Printing API (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Pretty Printing API (Debugging with GDB)
lang: en
resource-type: document
title: Pretty Printing API (Debugging with GDB)
---
::: header
Next: [Selecting Pretty-Printers](Selecting-Pretty_002dPrinters.html#Selecting-Pretty_002dPrinters)]
:::

---

#### 23.3.2.5 Pretty Printing API

A pretty-printer is just an object that holds a value and implements a specific interface, defined here. An example output is provided (see [Pretty Printing](Pretty-Printing.html#Pretty-Printing)).

Function: **pretty_printer.children** *(self)*

:   [GDB] will call this method on a pretty-printer to compute the children of the pretty-printer's value.

```
This method must return an object conforming to the Python iterator protocol. Each item returned by the iterator must be a tuple holding two elements. The first element is the "name" of the child; the second element is the child's value. The value can be any Python object which is convertible to a [GDB] value.

This method is optional. If it does not exist, [GDB] will act as though the value has no children.

For efficiency, the `children` method should lazily compute its results. This will let [GDB] read as few elements as necessary, for example when various print settings (see [Print Settings](Print-Settings.html#Print-Settings)) or `-var-list-children` (see [GDB/MI Variable Objects](GDB_002fMI-Variable-Objects.html#GDB_002fMI-Variable-Objects)) limit the number of elements to be displayed.

Children may be hidden from display based on the value of '`set print max-depth`' (see [Print Settings](Print-Settings.html#Print-Settings)).
```

```
<!-- -->
```

Function: **pretty_printer.display_hint** *(self)*

:   The CLI may call this method and use its result to change the formatting of a value. The result will also be supplied to an MI consumer as a '`displayhint`' attribute of the variable being printed.

```
This method is optional. If it does exist, this method must return a string or the special value `None`.

Some display hints are predefined by [GDB]:

'`array`'

:   Indicate that the object being printed is "array-like". The CLI uses this to respect parameters such as `set print elements` and `set print array`.

'`map`'

:   Indicate that the object being printed is "map-like", and that the children of this value can be assumed to alternate between keys and values.

'`string`'

:   Indicate that the object being printed is "string-like". If the printer's `to_string` method returns a Python string of some kind, then [GDB] will call its internal language-specific string-printing function to format the string. For the CLI this means adding quotation marks, possibly escaping some characters, respecting `set print elements`, and the like.

The special value `None` causes [GDB] to apply the default display rules.
```

```
<!-- -->
```

Function: **pretty_printer.to_string** *(self)*

:   [GDB] will call this method to display the string representation of the value passed to the object's constructor.

```
When printing from the CLI, if the `to_string` method exists, then [GDB] will prepend its result to the values returned by `children`. Exactly how this formatting is done is dependent on the display hint, and may change as more hints are added. Also, depending on the print settings (see [Print Settings](Print-Settings.html#Print-Settings)), the CLI may print just the result of `to_string` in a stack trace, omitting the result of `children`.

If this method returns a string, it is printed verbatim.

Otherwise, if this method returns an instance of `gdb.Value`, then [GDB] prints this value. This may result in a call to another pretty-printer.

If instead the method returns a Python value which is convertible to a `gdb.Value`, then [GDB] performs the conversion and prints the resulting value. Again, this may result in a call to another pretty-printer. Python scalars (integers, floats, and booleans) and strings are convertible to `gdb.Value`; other types are not.

Finally, if this method returns `None` then no further operations are peformed in this method and nothing is printed.

If the result is not one of these types, an exception is raised.
```

[GDB] provides a function which can be used to look up the default pretty-printer for a `gdb.Value`:

Function: **gdb.default_visualizer** *(value)*

:   This function takes a `gdb.Value` object as an argument. If a pretty-printer for this value exists, then it is returned. If no such printer exists, then this returns `None`.

Normally, a pretty-printer can respect the user's print settings (including temporarily applied settings, such as '`/x`') simply by calling `Value.format_string` (see [Values From Inferior](Values-From-Inferior.html#Values-From-Inferior)). However, these settings can also be queried directly:

Function: **gdb.print_options** *()*

:   Return a dictionary whose keys are the valid keywords that can be given to `Value.format_string`, and whose values are the user's settings. During a `print` or other operation, the values will reflect any flags that are temporarily in effect.

```
::: smallexample
``` smallexample
(gdb) python print (gdb.print_options ()['max_elements'])
200
```

:::

```

---

::: header
Next: [Selecting Pretty-Printers](Selecting-Pretty_002dPrinters.html#Selecting-Pretty_002dPrinters)]
:::
```
