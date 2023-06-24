---
tip: translate by openai@2023-06-23 20:58:02
...
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

> *明确的位置*允许用户使用选项-值对直接指定源位置的参数。


Explicit locations are useful when several functions, labels, or file names have the same name (base name for files) in the program's sources. In these cases, explicit locations point to the source line you meant more accurately and unambiguously. Also, using explicit locations might be faster in large programs.

> 明确的位置在程序源码中有多个函数、标签或文件名（文件的基本名称）具有相同名称时非常有用。在这些情况下，明确的位置更准确、更清晰地指向您所指的源行。此外，在大型程序中使用明确的位置可能更快。


For example, the linespec '`foo:bar` must search either the file system or the symbol table to know.

> 例如，线规'foo:bar'必须搜索文件系统或符号表以知晓。


The list of valid explicit location options is summarized in the following table:

> 以下表格总结了有效的明确位置选项列表：

`-source filename`


:   The value specifies the source file name. To differentiate between files with the same base name, prepend as many directories as is necessary to uniquely identify the desired file, e.g., `foo/bar/baz.c` will use the first file it finds with the given base name. This option requires the use of either `-function` or `-line`.

> 指定的值是源文件名。为了区分具有相同基本名称的文件，需要预先添加足够多的目录以唯一标识所需的文件，例如，`foo/bar/baz.c`将使用给定基本名称的第一个文件。此选项需要使用`-function`或`-line`。

`-function function`


:   The value specifies the name of a function. Operations on function locations unmodified by other options (such as `-label` or `-line`) refer to the line that begins the body of the function. In C, for example, this is the line with the open brace.

> 指定的值是一个函数的名称。其他选项（如`-label`或`-line`）未修改的函数位置上的操作引用了函数体开始的行。例如，在C中，这是带有开括号的行。

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

> 指定的值为标签的名称。当未指定函数名称时，将在当前选定的堆栈帧的函数中搜索标签。

`-line number`


:   The value specifies a line offset for the location. The offset may either be absolute (`-line 3`) or relative (`-line +3`), depending on the command. When specified without any other options, the line offset is relative to the current line.

> 值指定了位置的行偏移量。偏移量可以是绝对的（`-line 3`）或相对的（`-line +3`），取决于命令。如果没有指定其他选项，则行偏移量是相对于当前行的。


Explicit location options may be abbreviated by omitting any non-unique trailing characters from the option name, e.g., [break [-s].

> 可以通过省略选项名称中的任何非唯一尾随字符来缩写明确位置选项，例如[break [-s]。

---

::: header
Next: [Address Locations](Address-Locations.html#Address-Locations)]
:::
