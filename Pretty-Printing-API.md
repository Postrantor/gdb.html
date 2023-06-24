---
tip: translate by openai@2023-06-24 01:08:23
...
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

> 一个漂亮的打印机只是一个保存值并实现特定接口的对象，这里定义了该接口。提供了一个示例输出（请参阅[漂亮打印](Pretty-Printing.html#Pretty-Printing))。

Function: **pretty_printer.children** *(self)*


:   [GDB] will call this method on a pretty-printer to compute the children of the pretty-printer's value.

> GDB 将调用此方法来计算美化打印机的值的子项。

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

> 命令行界面可以调用此方法，并使用其结果更改值的格式。 结果还将作为打印变量的“displayhint”属性提供给MI消费者。

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

> GDB將會調用這個方法來顯示傳遞給對象構造函數的值的字符串表示形式。

```
When printing from the CLI, if the `to_string` method exists, then [GDB] will prepend its result to the values returned by `children`. Exactly how this formatting is done is dependent on the display hint, and may change as more hints are added. Also, depending on the print settings (see [Print Settings](Print-Settings.html#Print-Settings)), the CLI may print just the result of `to_string` in a stack trace, omitting the result of `children`.

If this method returns a string, it is printed verbatim.

Otherwise, if this method returns an instance of `gdb.Value`, then [GDB] prints this value. This may result in a call to another pretty-printer.

If instead the method returns a Python value which is convertible to a `gdb.Value`, then [GDB] performs the conversion and prints the resulting value. Again, this may result in a call to another pretty-printer. Python scalars (integers, floats, and booleans) and strings are convertible to `gdb.Value`; other types are not.

Finally, if this method returns `None` then no further operations are peformed in this method and nothing is printed.

If the result is not one of these types, an exception is raised.
```


[GDB] provides a function which can be used to look up the default pretty-printer for a `gdb.Value`:

> [GDB]提供了一个函数，可用于查找`gdb.Value`的默认格式化程序：

Function: **gdb.default_visualizer** *(value)*


:   This function takes a `gdb.Value` object as an argument. If a pretty-printer for this value exists, then it is returned. If no such printer exists, then this returns `None`.

> 这个函数接受一个`gdb.Value`对象作为参数。如果这个值有对应的美化打印器，则返回该打印器；如果没有，则返回`None`。


Normally, a pretty-printer can respect the user's print settings (including temporarily applied settings, such as '`/x`') simply by calling `Value.format_string` (see [Values From Inferior](Values-From-Inferior.html#Values-From-Inferior)). However, these settings can also be queried directly:

> 通常，一个漂亮的打印机可以通过调用“Value.format_string”（参见[来自下级的值]（Values-From-Inferior.html#Values-From-Inferior））来尊重用户的打印设置（包括暂时应用的设置，如“/x”）。但是，这些设置也可以直接查询。

Function: **gdb.print_options** *()*


:   Return a dictionary whose keys are the valid keywords that can be given to `Value.format_string`, and whose values are the user's settings. During a `print` or other operation, the values will reflect any flags that are temporarily in effect.

> 返回一个字典，其键是可以给`Value.format_string`提供的有效关键字，其值是用户的设置。在`打印`或其他操作期间，值将反映任何暂时有效的标志。

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
