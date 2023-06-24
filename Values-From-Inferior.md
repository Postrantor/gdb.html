---
tip: translate by openai@2023-06-24 04:38:56
...
---
description: Values From Inferior (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Values From Inferior (Debugging with GDB)
lang: en
resource-type: document
title: Values From Inferior (Debugging with GDB)
---
::: header
Next: [Types In Python](Types-In-Python.html#Types-In-Python)]
:::

---

#### 23.3.2.3 Values From Inferior


[GDB] uses this object for its internal bookkeeping of the inferior's values, and for fetching values when necessary.

> [GDB]使用这个对象来记录下被控制程序的值，并在必要时获取值。


Inferior values that are simple scalars can be used directly in Python expressions that are valid for the value's data type. Here's an example for an integer or floating-point value `some_val`:

> 简单标量的较低值可以直接用于与该值数据类型有效的Python表达式中。这里是一个整数或浮点值`some_val`的例子：

::: smallexample

```bash
bar = some_val + 2
```

:::


As result of this, `bar` will also be a `gdb.Value` object whose values are of the same type as those of `some_val`. Valid Python operations can also be performed on `gdb.Value` objects representing a `struct` or `class` object. For such cases, the overloaded operator (if present), is used to perform the operation. For example, if `val1` and `val2` are `gdb.Value` objects representing instances of a `class` which overloads the `+` operator, then one can use the `+` operator in their Python script as follows:

> 由此，`bar`也将是一个`gdb.Value`对象，其值的类型与`some_val`的值相同。还可以对代表`struct`或`class`对象的`gdb.Value`对象执行有效的Python操作。对于这种情况，将使用重载操作符（如果存在）执行操作。例如，如果`val1`和`val2`是代表重载`+`运算符的`class`的实例的`gdb.Value`对象，则可以在其Python脚本中使用`+`运算符，如下所示：

::: smallexample

```bash
val3 = val1 + val2
```

:::


The result of the operation `val3` is also a `gdb.Value` object corresponding to the value returned by the overloaded `+` operator. In general, overloaded operators are invoked for the following operations: `+` (binary addition), `-` (binary subtraction), `*` (multiplication), `/`, `%`, `<<`, `>>`, `|`, `&`, `^`.

> 操作`val3`的结果也是一个`gdb.Value`对象，对应于重载的`+`操作符返回的值。通常，重载的操作符用于以下操作：`+`（二元加法）、`-`（二元减法）、`*`（乘法）、`/`、`%`、`<<`、`>>`、`|`、`&`、`^`。


Inferior values that are structures or instances of some class can be accessed using the Python *dictionary syntax*. For example, if `some_val` is a `gdb.Value` instance holding a structure, you can access its `foo` element with:

> 可以使用Python字典语法访问低级值（它们是某个类的结构或实例）。例如，如果`some_val`是一个`gdb.Value`实例，它持有一个结构，你可以使用以下方式访问它的`foo`元素：

::: smallexample

```bash
bar = some_val['foo']
```

:::


Again, `bar` will also be a `gdb.Value` object. Structure elements can also be accessed by using `gdb.Field` objects as subscripts (see [Types In Python](Types-In-Python.html#Types-In-Python), for more information on `gdb.Field` objects). For example, if `foo_field` is a `gdb.Field` object corresponding to element `foo` of the above structure, then `bar` can also be accessed as follows:

> 再次，`bar`也将是一个`gdb.Value`对象。结构元素也可以通过使用`gdb.Field`对象作为下标来访问（有关`gdb.Field`对象的更多信息，请参见[Python中的类型](Types-In-Python.html#Types-In-Python)）。例如，如果`foo_field`是上述结构中的元素`foo`的`gdb.Field`对象，那么`bar`也可以通过以下方式访问：

::: smallexample

```bash
bar = some_val[foo_field]
```

:::


A `gdb.Value` that represents a function can be executed via inferior function call. Any arguments provided to the call must match the function's prototype, and must be provided in the order specified by that prototype.

> 一个表示函数的`gdb.Value`可以通过下级函数调用来执行。提供给调用的任何参数都必须与函数的原型匹配，并且必须按照该原型指定的顺序提供。


For example, `some_val` is a `gdb.Value` instance representing a function that takes two integers as arguments. To execute this function, call it like so:

> 例如，`some_val`是一个`gdb.Value`实例，表示一个接受两个整数作为参数的函数。要执行此函数，请按如下方式调用它：

::: smallexample

```bash
result = some_val (10,20)
```

:::

Any values returned from a function call will be stored as a `gdb.Value`.

The following attributes are provided:

Variable: **Value.address**


:   If this object is addressable, this read-only attribute holds a `gdb.Value` object representing the address. Otherwise, this attribute holds `None`.

> 如果这个对象是可寻址的，这个只读属性持有一个`gdb.Value`对象来表示地址。否则，这个属性持有`None`。

Variable: **Value.is_optimized_out**


:   This read-only boolean attribute is true if the compiler optimized out this value, thus it is not available for fetching from the inferior.

> 这个只读布尔属性如果编译器优化掉了这个值，则为true，因此无法从下属中获取它。

```
<!-- -->
```

Variable: **Value.type**


:   The type of this `gdb.Value`. The value of this attribute is a `gdb.Type` object (see [Types In Python](Types-In-Python.html#Types-In-Python)).

> 这个`gdb.Value`的类型。该属性的值是一个`gdb.Type`对象（参见[Python中的类型](Types-In-Python.html#Types-In-Python)）。

```
<!-- -->
```

Variable: **Value.dynamic_type**


:   The dynamic type of this `gdb.Value`. This uses the object's virtual table and the C++ run-time type information (RTTI) to determine the dynamic type of the value. If this value is of class type, it will return the class in which the value is embedded, if any. If this value is of pointer or reference to a class type, it will compute the dynamic type of the referenced object, and return a pointer or reference to that type, respectively. In all other cases, it will return the value's static type.

> 这个`gdb.Value`的动态类型。它使用对象的虚表和C++运行时类型信息（RTTI）来确定值的动态类型。如果这个值是类类型，它将返回包含值的类（如果有的话）。如果这个值是指向类类型的指针或引用，它将计算引用对象的动态类型，并分别返回指向该类型的指针或引用。在所有其他情况下，它将返回值的静态类型。

```
Note that this feature will only work when debugging a C++ program that includes RTTI for the object in question. Otherwise, it will just return the static type of the value as in [ptype foo] (see [ptype](Symbols.html#Symbols)).
```

```
<!-- -->
```

Variable: **Value.is_lazy**


:   The value of this read-only boolean attribute is `True` if this `gdb.Value` has not yet been fetched from the inferior. [GDB] does not fetch values until necessary, for efficiency. For example:

> 此只读布尔属性的值为“真”，如果此“gdb.Value”尚未从次级获取。为了提高效率，[GDB]不会在必要时获取值。例如：

```
::: smallexample
``` smallexample
myval = gdb.parse_and_eval ('somevar')
```

:::

The value of `somevar` is not fetched at this time. It will be fetched when the value is needed, or when the `fetch_lazy` method is invoked.

```

The following methods are provided:

Function: **Value.__init__** *(val)*


:   Many Python values can be converted directly to a `gdb.Value` via this object initializer. Specifically:

> 许多Python值可以通过这个对象初始化器直接转换为gdb.Value。具体来说：

```

Python boolean

:   A Python boolean is converted to the boolean type from the current language.

Python integer

:   A Python integer is converted to the C `long` type for the current architecture.

Python long

:   A Python long is converted to the C `long long` type for the current architecture.

Python float

:   A Python float is converted to the C `double` type for the current architecture.

Python string

:   A Python string is converted to a target string in the current target language using the current target encoding. If a character cannot be represented in the current target encoding, then an exception is thrown.

`gdb.Value`

:   If `val` is a `gdb.Value`, then a copy of the value is made.

`gdb.LazyString`

:   If `val` is a `gdb.LazyString` (see [Lazy Strings In Python](Lazy-Strings-In-Python.html#Lazy-Strings-In-Python)), then the lazy string's `value` method is called, and its result is used.

```

```

<!-- -->

```

Function: **Value.__init__** *(val, type)*


:   This second form of the `gdb.Value` constructor returns a `gdb.Value` of type `type`.

> 这个`gdb.Value`构造函数的第二种形式返回一个类型为`type`的`gdb.Value`。

```

If `type` was not passed at all.

```

```

<!-- -->

```

Function: **Value.assign** *(rhs)*


:   Assign `rhs` to this value, and return `None`. If this value cannot be assigned to, or if the assignment is invalid for some reason (for example a type-checking failure), an exception will be thrown.

> 将`rhs`分配给这个值，并返回`None`。如果无法分配此值或由于某种原因（例如类型检查失败）分配无效，则会抛出异常。

```

<!-- -->

```

Function: **Value.cast** *(type)*


:   Return a new instance of `gdb.Value` that is the result of casting this instance to the type described by `type`, which must be a `gdb.Type` object. If the cast cannot be performed for some reason, this method throws an exception.

> 返回一个新的`gdb.Value`实例，它是将此实例按照`type`（必须是`gdb.Type`对象）描述的类型进行转换的结果。如果由于某种原因无法执行转换，则此方法会抛出异常。

```

<!-- -->

```

Function: **Value.dereference** *()*


:   For pointer data types, this method returns a new `gdb.Value` object whose contents is the object pointed to by the pointer. For example, if `foo` is a C pointer to an `int`, declared in your C program as

> 对于指针数据类型，此方法返回一个新的`gdb.Value`对象，其内容是指针指向的对象。例如，如果`foo`是在C程序中声明的一个指向`int`的C指针，

```

::: smallexample

```bash
int *foo;
```

:::

then you can use the corresponding `gdb.Value` to access what `foo` points to like this:

::: smallexample

```bash
bar = foo.dereference ()
```

:::

The result `bar` will be a `gdb.Value` object holding the value pointed to by `foo`.

A similar function `Value.referenced_value` exists which also returns `gdb.Value` objects corresponding to the values pointed to by pointer values (and additionally, values referenced by reference values). However, the behavior of `Value.dereference` differs from `Value.referenced_value` by the fact that the behavior of `Value.dereference` is identical to applying the C unary operator `*` on a given value. For example, consider a reference to a pointer `ptrref`, declared in your C++ program as

::: smallexample

```bash
typedef int *intptr;
...
int val = 10;
intptr ptr = &val;
intptr &ptrref = ptr;
```

:::

Though `ptrref` is a reference value, one can apply the method `Value.dereference` to the `gdb.Value` object corresponding to it and obtain a `gdb.Value` which is identical to that corresponding to `val`. However, if you apply the method `Value.referenced_value`, the result would be a `gdb.Value` object identical to that corresponding to `ptr`.

::: smallexample

```bash
py_ptrref = gdb.parse_and_eval ("ptrref")
py_val = py_ptrref.dereference ()
py_ptr = py_ptrref.referenced_value ()
```

:::

The `gdb.Value` object `py_val` is identical to that corresponding to `val`, and `py_ptr` is identical to that corresponding to `ptr`. In general, `Value.dereference` can be applied whenever the C unary operator `*` can be applied to the corresponding C value. For those cases where applying both `Value.dereference` and `Value.referenced_value` is allowed, the results obtained need not be identical (as we have seen in the above example). The results are however identical when applied on `gdb.Value` objects corresponding to pointers (`gdb.Value` objects with type code `TYPE_CODE_PTR`) in a C/C++ program.

```

```

<!-- -->

```

Function: **Value.referenced_value** *()*


:   For pointer or reference data types, this method returns a new `gdb.Value` object corresponding to the value referenced by the pointer/reference value. For pointer data types, `Value.dereference` and `Value.referenced_value` produce identical results. The difference between these methods is that `Value.dereference` cannot get the values referenced by reference values. For example, consider a reference to an `int`, declared in your C++ program as

> 对于指针或引用数据类型，此方法返回一个新的`gdb.Value`对象，该对象对应于指针/引用值所引用的值。 对于指针数据类型，`Value.dereference`和`Value.referenced_value`产生相同的结果。 这些方法之间的区别在于`Value.dereference`无法获取引用值引用的值。 例如，在您的C ++程序中声明一个对`int`的引用

```

::: smallexample

```bash
int val = 10;
int &ref = val;
```

:::

then applying `Value.dereference` to the `gdb.Value` object corresponding to `ref` will result in an error, while applying `Value.referenced_value` will result in a `gdb.Value` object identical to that corresponding to `val`.

::: smallexample

```bash
py_ref = gdb.parse_and_eval ("ref")
er_ref = py_ref.dereference ()       # Results in error
py_val = py_ref.referenced_value ()  # Returns the referenced value
```

:::

The `gdb.Value` object `py_val` is identical to that corresponding to `val`.

```

```

<!-- -->

```

Function: **Value.reference_value** *()*


:   Return a `gdb.Value` object which is a reference to the value encapsulated by this instance.

> 返回一个`gdb.Value`对象，它是对此实例封装的值的引用。

```

<!-- -->

```

Function: **Value.const_value** *()*


:   Return a `gdb.Value` object which is a `const` version of the value encapsulated by this instance.

> 返回一个`gdb.Value`对象，它是由此实例封装的值的`const`版本。

```

<!-- -->

```

Function: **Value.dynamic_cast** *(type)*


:   Like `Value.cast`, but works as if the C++ `dynamic_cast` operator were used. Consult a C++ reference for details.

> 像`Value.cast`一样，但就像使用C++的`dynamic_cast`操作符一样工作。有关详细信息，请参阅C++参考资料。

```

<!-- -->

```

Function: **Value.reinterpret_cast** *(type)*


:   Like `Value.cast`, but works as if the C++ `reinterpret_cast` operator were used. Consult a C++ reference for details.

> 就像“Value.cast”一样，但是表现得就像使用了C++的“reinterpret_cast”操作符一样。有关详细信息，请参阅C++参考资料。

```

<!-- -->

```

Function: **Value.format_string** *(\...)*


:   Convert a `gdb.Value` to a string, similarly to what the `print` command does. Invoked with no arguments, this is equivalent to calling the `str` function on the `gdb.Value`. The representation of the same value may change across different versions of [GDB], so you shouldn't, for instance, parse the strings returned by this method.

> 将`gdb.Value`转换为字符串，类似于`print`命令所做的。如果没有参数调用，这相当于在`gdb.Value`上调用`str`函数。同一个值的表示可能会随着[GDB]的不同版本而改变，因此您不应该解析此方法返回的字符串。

```

All the arguments are keyword only. If an argument is not specified, the current global default setting is used.

`raw`

:   `True` if pretty-printers (see [Pretty Printing](Pretty-Printing.html#Pretty-Printing)) should not be used to format the value. `False` if enabled pretty-printers matching the type represented by the `gdb.Value` should be used to format it.

`pretty_arrays`

:   `True` if arrays should be pretty printed to be more convenient to read, `False` if they shouldn't (see `set print array` in [Print Settings](Print-Settings.html#Print-Settings)).

`pretty_structs`

:   `True` if structs should be pretty printed to be more convenient to read, `False` if they shouldn't (see `set print pretty` in [Print Settings](Print-Settings.html#Print-Settings)).

`array_indexes`

:   `True` if array indexes should be included in the string representation of arrays, `False` if they shouldn't (see `set print array-indexes` in [Print Settings](Print-Settings.html#Print-Settings)).

`symbols`

:   `True` if the string representation of a pointer should include the corresponding symbol name (if one exists), `False` if it shouldn't (see `set print symbol` in [Print Settings](Print-Settings.html#Print-Settings)).

`unions`

:   `True` if unions which are contained in other structures or unions should be expanded, `False` if they shouldn't (see `set print union` in [Print Settings](Print-Settings.html#Print-Settings)).

`address`

:   `True` if the string representation of a pointer should include the address, `False` if it shouldn't (see `set print address` in [Print Settings](Print-Settings.html#Print-Settings)).

`nibbles`

:   `True` if binary values should be displayed in groups of four bits, known as nibbles. `False` if it shouldn't (see [set print nibbles](Print-Settings.html#Print-Settings)).

`deref_refs`

:   `True` if C++ references should be resolved to the value they refer to, `False` (the default) if they shouldn't. Note that, unlike for the `print` command, references are not automatically expanded when using the `format_string` method or the `str` function. There is no global `print` setting to change the default behaviour.

`actual_objects`

:   `True` if the representation of a pointer to an object should identify the *actual* (derived) type of the object rather than the *declared* type, using the virtual function table. `False` if the *declared* type should be used. (See `set print object` in [Print Settings](Print-Settings.html#Print-Settings)).

`static_members`

:   `True` if static members should be included in the string representation of a C++ object, `False` if they shouldn't (see `set print static-members` in [Print Settings](Print-Settings.html#Print-Settings)).

`max_characters`

:   Number of string characters to print, `0` to follow `max_elements`, or `UINT_MAX` to print an unlimited number of characters (see `set print characters` in [Print Settings](Print-Settings.html#Print-Settings)).

`max_elements`

:   Number of array elements to print, or `0` to print an unlimited number of elements (see `set print elements` in [Print Settings](Print-Settings.html#Print-Settings)).

`max_depth`

:   The maximum depth to print for nested structs and unions, or `-1` to print an unlimited number of elements (see `set print max-depth` in [Print Settings](Print-Settings.html#Print-Settings)).

`repeat_threshold`

:   Set the threshold for suppressing display of repeated array elements, or `0` to represent all elements, even if repeated. (See `set print repeats` in [Print Settings](Print-Settings.html#Print-Settings)).

`format`

:   A string containing a single character representing the format to use for the returned string. For instance, `'x'` is equivalent to using the [GDB] command `print` with the `/x` option and formats the value as a hexadecimal number.

`styling`

:   `True` if [GDB] only styles some value contents, so not every output string will contain escape sequences.

```
When `False`, which is the default, no output styling is applied.
```

`summary`

:   `True` when just a summary should be printed. In this mode, scalar values are printed in their entirety, but aggregates such as structures or unions are omitted. This mode is used by `set print frame-arguments scalars` (see [Print Settings](Print-Settings.html#Print-Settings)).

```

```

<!-- -->

```

)*


:   If this `gdb.Value` represents a string, then this method converts the contents to a Python string. Otherwise, this method will throw an exception.

> 如果这个`gdb.Value`代表一个字符串，那么这个方法会将内容转换为Python字符串。否则，此方法将抛出异常。

```

Values are interpreted as strings according to the rules of the current language. If the optional length argument is given, the string will be converted to that length, and will include any embedded zeroes that the string may contain. Otherwise, for languages where the string is zero-terminated, the entire string will be converted.

For example, in C-like languages, a value is a string if it is a pointer to or an array of characters or ints of type `wchar_t`, `char16_t`, or `char32_t`.

If the optional `encoding` is the empty string, then either the `target-charset` (see [Character Sets](Character-Sets.html#Character-Sets)) will be used, or a language-specific encoding will be used, if the current language is able to supply one.

The optional `errors` argument is the same as the corresponding argument to Python's `string.decode` method.

If the optional `length` argument is given, the string will be fetched and converted to the given length.

```

```

<!-- -->

```

)*


:   If this `gdb.Value` represents a string, then this method converts the contents to a `gdb.LazyString` (see [Lazy Strings In Python](Lazy-Strings-In-Python.html#Lazy-Strings-In-Python)). Otherwise, this method will throw an exception.

> 如果这个`gdb.Value`代表一个字符串，那么这个方法将内容转换为`gdb.LazyString`（参见[Python中的懒惰字符串]（Lazy-Strings-In-Python.html#Lazy-Strings-In-Python））。否则，此方法将引发异常。

```

If the optional `encoding` will raise an error.

When a lazy string is printed, the [GDB] please see [Character Sets](Character-Sets.html#Character-Sets).

If the optional `length` argument is not provided, the string will be fetched and encoded until a null of appropriate width is found.

```

```

<!-- -->

```

Function: **Value.fetch_lazy** *()*


:   If the `gdb.Value` object is currently a lazy value (`gdb.Value.is_lazy` is `True`), then the value is fetched from the inferior. Any errors that occur in the process will produce a Python exception.

> 如果`gdb.Value`对象当前是懒惰值（`gdb.Value.is_lazy`为`True`），那么该值将从下级获取。在此过程中发生的任何错误都会产生一个Python异常。

```

If the `gdb.Value` object is not a lazy value, this method has no effect.

This method does not return a value.

```

---

::: header
Next: [Types In Python](Types-In-Python.html#Types-In-Python)]
:::
```
