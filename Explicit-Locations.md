---
description: Explicit Locations (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Explicit Locations (Debugging with GDB)
lang: en
resource-type: document
title: Explicit Locations (Debugging with GDB)
---
::: header
Next: [Address Locations](Address-Locations.html#Address-Locations)]
:::

---

#### 9.2.2 Explicit Locations

*Explicit locations* allow the user to directly specify the source location's parameters using option-value pairs.

Explicit locations are useful when several functions, labels, or file names have the same name (base name for files) in the program's sources. In these cases, explicit locations point to the source line you meant more accurately and unambiguously. Also, using explicit locations might be faster in large programs.

For example, the linespec '`foo:bar` must search either the file system or the symbol table to know.

The list of valid explicit location options is summarized in the following table:

`-source filename`

:   The value specifies the source file name. To differentiate between files with the same base name, prepend as many directories as is necessary to uniquely identify the desired file, e.g., `foo/bar/baz.c` will use the first file it finds with the given base name. This option requires the use of either `-function` or `-line`.

`-function function`

:   The value specifies the name of a function. Operations on function locations unmodified by other options (such as `-label` or `-line`) refer to the line that begins the body of the function. In C, for example, this is the line with the open brace.

```
By default, in C++ and Ada, `function` in all scopes. For C++, this means in all namespaces and classes. For Ada, this means in all packages.

For example, assuming a program with C++ symbols named `A::B::func` and `B::func`, both commands [break [-function] set a breakpoint on both symbols.

You can use the [-qualified] flag to override this (see below).
```

`-qualified`

:   This flag makes [GDB] as a complete fully-qualified name.

```
For example, assuming a C++ program with symbols named `A::B::func` and `B::func`, the [break [-qualified] command sets a breakpoint on `B::func`, only.

(Note: the [-qualified].)
```

`-label label`

:   The value specifies the name of a label. When the function name is not specified, the label is searched in the function of the currently selected stack frame.

`-line number`

:   The value specifies a line offset for the location. The offset may either be absolute (`-line 3`) or relative (`-line +3`), depending on the command. When specified without any other options, the line offset is relative to the current line.

Explicit location options may be abbreviated by omitting any non-unique trailing characters from the option name, e.g., [break [-s].

---

::: header
Next: [Address Locations](Address-Locations.html#Address-Locations)]
:::
