---
description: Guile Pretty Printing API (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Guile Pretty Printing API (Debugging with GDB)
lang: en
resource-type: document
title: Guile Pretty Printing API (Debugging with GDB)
---
::: header
Next: [Selecting Guile Pretty-Printers](Selecting-Guile-Pretty_002dPrinters.html#Selecting-Guile-Pretty_002dPrinters)]
:::

---

#### 23.4.3.8 Guile Pretty Printing API

An example output is provided (see [Pretty Printing](Pretty-Printing.html#Pretty-Printing)).

A pretty-printer is represented by an object of type \<gdb:pretty-printer\>. Pretty-printer objects are created with `make-pretty-printer`.

The following pretty-printer-related procedures are provided by the `(gdb)` module:

Scheme Procedure: **make-pretty-printer** *name lookup-function*

:   Return a `<gdb:pretty-printer>` object named `name`.

```
`lookup-function` returns `#f`.
```

```
<!-- -->
```

Scheme Procedure: **pretty-printer?** *object*

:   Return `#t` if `object` is a `<gdb:pretty-printer>` object. Otherwise return `#f`.

```
<!-- -->
```

Scheme Procedure: **pretty-printer-enabled?** *pretty-printer*

:   Return `#t` if `pretty-printer` is enabled. Otherwise return `#f`.

```
<!-- -->
```

Scheme Procedure: **set-pretty-printer-enabled!** *pretty-printer flag*

:   Set the enabled flag of `pretty-printer`. The value returned is unspecified.

```
<!-- -->
```

Scheme Procedure: **pretty-printers**

:   Return the list of global pretty-printers.

```
<!-- -->
```

Scheme Procedure: **set-pretty-printers!** *pretty-printers*

:   Set the list of global pretty-printers to `pretty-printers`. The value returned is unspecified.

```
<!-- -->
```

Scheme Procedure: **make-pretty-printer-worker** *display-hint to-string children*

:   Return an object of type `<gdb:pretty-printer-worker>`.

```
This function takes three parameters:

'`display-hint`'

:   `display-hint`:

    '`array`'

    :   Indicate that the object being printed is "array-like". The CLI uses this to respect parameters such as `set print elements` and `set print array`.

    '`map`'

    :   Indicate that the object being printed is "map-like", and that the children of this value can be assumed to alternate between keys and values.

    '`string`'

    :   Indicate that the object being printed is "string-like". If the printer's `to-string` function returns a Guile string of some kind, then [GDB] will call its internal language-specific string-printing function to format the string. For the CLI this means adding quotation marks, possibly escaping some characters, respecting `set print elements`, and the like.

'`to-string`'

:   `to-string` is either a function of one parameter, the `<gdb:pretty-printer-worker>` object, or `#f`.

    When printing from the CLI, if the `to-string` method exists, then [GDB] will prepend its result to the values returned by `children`. Exactly how this formatting is done is dependent on the display hint, and may change as more hints are added. Also, depending on the print settings (see [Print Settings](Print-Settings.html#Print-Settings)), the CLI may print just the result of `to-string` in a stack trace, omitting the result of `children`.

    If this method returns a string, it is printed verbatim.

    Otherwise, if this method returns an instance of `<gdb:value>`, then [GDB] prints this value. This may result in a call to another pretty-printer.

    If instead the method returns a Guile value which is convertible to a `<gdb:value>`, then [GDB] performs the conversion and prints the resulting value. Again, this may result in a call to another pretty-printer. Guile scalars (integers, floats, and booleans) and strings are convertible to `<gdb:value>`; other types are not.

    Finally, if this method returns `#f` then no further operations are peformed in this method and nothing is printed.

    If the result is not one of these types, an exception is raised.

    `to-string` to print the value.

'`children`'

:   `children` is either a function of one parameter, the `<gdb:pretty-printer-worker>` object, or `#f`.

    [GDB] will call this function on a pretty-printer to compute the children of the pretty-printer's value.

    This function must return a \<gdb:iterator\> object. Each item returned by the iterator must be a tuple holding two elements. The first element is the "name" of the child; the second element is the child's value. The value can be any Guile object which is convertible to a [GDB] value.

    If `children` will act as though the value has no children.

    Children may be hidden from display based on the value of '`set print max-depth`' (see [Print Settings](Print-Settings.html#Print-Settings)).
```

[GDB] provides a function which can be used to look up the default pretty-printer for a `<gdb:value>`:

Scheme Procedure: **default-visualizer** *value*

:   This function takes a `<gdb:value>` object as an argument. If a pretty-printer for this value exists, then it is returned. If no such printer exists, then this returns `#f`.

---

::: header
Next: [Selecting Guile Pretty-Printers](Selecting-Guile-Pretty_002dPrinters.html#Selecting-Guile-Pretty_002dPrinters)]
:::
