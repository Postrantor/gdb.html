---
tip: translate by openai@2023-06-23 15:30:30
...
---
description: Values From Inferior (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Values From Inferior (Debugging with GDB)
lang: en
resource-type: document
title: Values From Inferior (Debugging with GDB)
------------------------------------------------

::: header
Next: [Types In Python](Types-In-Python.html#Types-In-Python)]
:::

---

#### 23.3.2.3 Values From Inferior

[GDB] uses this object for its internal bookkeeping of the inferior's values, and for fetching values when necessary.

> [GDB]使用这个对象来跟踪下属的值的内部记账，并在必要时获取值。

Inferior values that are simple scalars can be used directly in Python expressions that are valid for the value's data type. Here's an example for an integer or floating-point value `some_val`:

> 简单的标量值可以直接用于与该值数据类型相符的 Python 表达式中。这里是一个整数或浮点值 `some_val` 的例子：

::: smallexample

```bash
bar = some_val + 2
```

:::

As result of this, `bar` will also be a `gdb.Value` object whose values are of the same type as those of `some_val`. Valid Python operations can also be performed on `gdb.Value` objects representing a `struct` or `class` object. For such cases, the overloaded operator (if present), is used to perform the operation. For example, if `val1` and `val2` are `gdb.Value` objects representing instances of a `class` which overloads the `+` operator, then one can use the `+` operator in their Python script as follows:

> 结果，'bar'也将是一个 gdb.Value 对象，其值与'some_val'的值类型相同。 对表示'struct'或'class'对象的 gdb.Value 对象也可以执行有效的 Python 操作。 对于这种情况，使用重载的运算符（如果存在）来执行操作。 例如，如果'val1'和'val2'是表示重载'+'运算符的类的实例的 gdb.Value 对象，那么可以在 Python 脚本中使用'+'运算符，如下所示：

::: smallexample

```bash
val3 = val1 + val2
```

:::

The result of the operation `val3` is also a `gdb.Value` object corresponding to the value returned by the overloaded `+` operator. In general, overloaded operators are invoked for the following operations: `+` (binary addition), `-` (binary subtraction), `*` (multiplication), `/`, `%`, `<<`, `>>`, `|`, `&`, `^`.

> 结果 `val3` 也是一个 `gdb.Value` 对象，对应于重载的 `+` 操作符返回的值。通常，重载的操作符被用于以下操作：`+`（二元加法）、`-`（二元减法）、`*`（乘法）、`/`、`%`、`<<`、`>>`、`|`、`&`、`^`。

Inferior values that are structures or instances of some class can be accessed using the Python *dictionary syntax*. For example, if `some_val` is a `gdb.Value` instance holding a structure, you can access its `foo` element with:

> Python 的字典语法可以访问较低级的值，它们是某个类的结构或实例。例如，如果 `some_val` 是一个 `gdb.Value` 实例，它保存着一个结构，你可以用：访问它的 `foo` 元素。

::: smallexample

```bash
bar = some_val['foo']
```

:::

Again, `bar` will also be a `gdb.Value` object. Structure elements can also be accessed by using `gdb.Field` objects as subscripts (see [Types In Python](Types-In-Python.html#Types-In-Python), for more information on `gdb.Field` objects). For example, if `foo_field` is a `gdb.Field` object corresponding to element `foo` of the above structure, then `bar` can also be accessed as follows:

> 再次，`bar` 也将是一个 `gdb.Value` 对象。结构元素也可以通过使用 `gdb.Field` 对象作为下标来访问（有关 `gdb.Field` 对象的更多信息，请参见 [Python 中的类型](Types-In-Python.html#Types-In-Python)）。例如，如果 `foo_field` 是一个对应于上述结构中的元素 `foo` 的 `gdb.Field` 对象，那么 `bar` 也可以如下访问：

::: smallexample

```bash
bar = some_val[foo_field]
```

:::

A `gdb.Value` that represents a function can be executed via inferior function call. Any arguments provided to the call must match the function's prototype, and must be provided in the order specified by that prototype.

> 一个表示函数的 `gdb.Value` 可以通过下级函数调用来执行。提供给调用的任何参数都必须与函数的原型匹配，并且必须按照原型指定的顺序提供。

For example, `some_val` is a `gdb.Value` instance representing a function that takes two integers as arguments. To execute this function, call it like so:

> 例如，`some_val` 是一个 `gdb.Value` 实例，表示一个接受两个整数作为参数的函数。要执行这个函数，可以这样调用它：

::: smallexample

```bash
result = some_val (10,20)
```

:::

Any values returned from a function call will be stored as a `gdb.Value`.

> 任何从函数调用返回的值都将存储为 `gdb.Value`。

The following attributes are provided:

> 以下属性提供：

Variable: **Value.address**

> 变量：**Value.address**

:   If this object is addressable, this read-only attribute holds a `gdb.Value` object representing the address. Otherwise, this attribute holds `None`.

> 如果这个对象是可寻址的，这个只读属性持有一个表示地址的 `gdb.Value` 对象。否则，这个属性持有 `None`。

Variable: **Value.is_optimized_out**

> 变量：**值.已优化外**

:   This read-only boolean attribute is true if the compiler optimized out this value, thus it is not available for fetching from the inferior.

> 这个只读的布尔属性如果编译器优化掉了这个值，那么它就不能从次级程序中获取，此时它的值为 true。

```

```

Variable: **Value.type**

> 变量：**值。类型**

:   The type of this `gdb.Value`. The value of this attribute is a `gdb.Type` object (see [Types In Python](Types-In-Python.html#Types-In-Python)).

> 这个 `gdb.Value` 的类型。该属性的值是一个 `gdb.Type` 对象（参见 [Python 中的类型](Types-In-Python.html#Types-In-Python)）。

```

```

Variable: **Value.dynamic_type**

> 变量：**Value.dynamic_type**

:   The dynamic type of this `gdb.Value`. This uses the object's virtual table and the C++ run-time type information (RTTI) to determine the dynamic type of the value. If this value is of class type, it will return the class in which the value is embedded, if any. If this value is of pointer or reference to a class type, it will compute the dynamic type of the referenced object, and return a pointer or reference to that type, respectively. In all other cases, it will return the value's static type.

> 这个 `gdb.Value` 的动态类型。它使用对象的虚表和 C++ 运行时类型信息（RTTI）来确定值的动态类型。如果这个值是类类型，它将返回嵌入值的类（如果有的话）。如果这个值是指向类类型的指针或引用，它将计算引用对象的动态类型，并分别返回指向该类型的指针或引用。在所有其他情况下，它将返回值的静态类型。

```
Note that this feature will only work when debugging a C++ program that includes RTTI for the object in question. Otherwise, it will just return the static type of the value as in [ptype foo] (see [ptype](Symbols.html#Symbols)).
```

```

```

Variable: **Value.is_lazy**

> 变量：**Value.is_lazy**

:   The value of this read-only boolean attribute is `True` if this `gdb.Value` has not yet been fetched from the inferior. [GDB] does not fetch values until necessary, for efficiency. For example:

> 这个只读布尔属性的值如果这个 GDB.Value 尚未从下级获取，则为 `True`。为了提高效率，[GDB]不会在必要时才获取值。例如：

```
::: smallexample
``` smallexample

myval = gdb.parse_and_eval ('somevar')

> 我的值 = gdb.parse_and_eval('somevar')
```

:::

The value of `somevar` is not fetched at this time. It will be fetched when the value is needed, or when the `fetch_lazy` method is invoked.

```


The following methods are provided:

> 以下方法提供：


Function: **Value.__init__** *(val)*

> 功能：**Value.__init__** *（val）*


:   Many Python values can be converted directly to a `gdb.Value` via this object initializer. Specifically:

> 许多Python值可以通过此对象初始化程序直接转换为gdb.Value。具体来说：

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

```


Function: **Value.__init__** *(val, type)*

> 函数：**Value.__init__** *（val，type）*


:   This second form of the `gdb.Value` constructor returns a `gdb.Value` of type `type`.

> 这个`gdb.Value`构造函数的第二种形式返回一个`type`类型的`gdb.Value`。

```

If `type` was not passed at all.

```

```

```


Function: **Value.assign** *(rhs)*

> 功能：**Value.assign** *（rhs）*


:   Assign `rhs` to this value, and return `None`. If this value cannot be assigned to, or if the assignment is invalid for some reason (for example a type-checking failure), an exception will be thrown.

> 将`rhs`分配给此值，并返回`None`。 如果无法分配此值，或者由于某种原因（例如类型检查失败）分配无效，则会抛出异常。

```

```


Function: **Value.cast** *(type)*

> 功能：**Value.cast**（类型）


:   Return a new instance of `gdb.Value` that is the result of casting this instance to the type described by `type`, which must be a `gdb.Type` object. If the cast cannot be performed for some reason, this method throws an exception.

> 返回一个`gdb.Value`的新实例，该实例是将此实例按照`type`描述的类型进行转换后的结果，`type`必须是一个`gdb.Type`对象。如果由于某种原因无法执行转换，此方法将抛出异常。

```

```


Function: **Value.dereference** *()*

> 函数：**Value.dereference** *（）*


:   For pointer data types, this method returns a new `gdb.Value` object whose contents is the object pointed to by the pointer. For example, if `foo` is a C pointer to an `int`, declared in your C program as

> 对于指针数据类型，此方法返回一个新的`gdb.Value`对象，其内容是指针指向的对象。例如，如果`foo`是在您的C程序中声明的指向`int`的C指针，

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

> bar = foo.取消引用()
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

> py_ptrref = gdb.parse_and_eval("ptrref") 
简体中文：py_ptrref = gdb.parse_and_eval("ptrref")

py_val = py_ptrref.dereference ()

> py_val = py_ptrref.取值()

py_ptr = py_ptrref.referenced_value ()

> py_ptr = py_ptrref.引用的值()
```

:::

The `gdb.Value` object `py_val` is identical to that corresponding to `val`, and `py_ptr` is identical to that corresponding to `ptr`. In general, `Value.dereference` can be applied whenever the C unary operator `*` can be applied to the corresponding C value. For those cases where applying both `Value.dereference` and `Value.referenced_value` is allowed, the results obtained need not be identical (as we have seen in the above example). The results are however identical when applied on `gdb.Value` objects corresponding to pointers (`gdb.Value` objects with type code `TYPE_CODE_PTR`) in a C/C++ program.

```

```

```


Function: **Value.referenced_value** *()*

> 功能：**Value.referenced_value** *（）*


:   For pointer or reference data types, this method returns a new `gdb.Value` object corresponding to the value referenced by the pointer/reference value. For pointer data types, `Value.dereference` and `Value.referenced_value` produce identical results. The difference between these methods is that `Value.dereference` cannot get the values referenced by reference values. For example, consider a reference to an `int`, declared in your C++ program as

> 对于指针或引用数据类型，此方法返回与指针/引用值引用的值相对应的新`gdb.Value`对象。对于指针数据类型，`Value.dereference`和`Value.referenced_value`产生相同的结果。这些方法之间的区别是`Value.dereference`无法获取引用值引用的值。例如，在您的C ++程序中声明对`int`的引用

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

> py_ref = gdb.parse_and_eval("ref")  # 翻译成简体中文：py_ref = gdb.parse_and_eval("ref")

er_ref = py_ref.dereference ()       # Results in error

> er_ref = py_ref.dereference() # 导致错误

py_val = py_ref.referenced_value ()  # Returns the referenced value

> py_val = py_ref.引用值()  # 返回引用值
```

:::

The `gdb.Value` object `py_val` is identical to that corresponding to `val`.

```

```

```


Function: **Value.reference_value** *()*

> 功能：**Value.reference_value** *（）*


:   Return a `gdb.Value` object which is a reference to the value encapsulated by this instance.

> 返回一个`gdb.Value`对象，它是对此实例封装的值的引用。

```

```


Function: **Value.const_value** *()*

> 功能：**Value.const_value** *（）*


:   Return a `gdb.Value` object which is a `const` version of the value encapsulated by this instance.

> 返回一个`gdb.Value`对象，它是由此实例封装的值的`const`版本。

```

```


Function: **Value.dynamic_cast** *(type)*

> 功能：**Value.dynamic_cast**（类型）


:   Like `Value.cast`, but works as if the C++ `dynamic_cast` operator were used. Consult a C++ reference for details.

> 像Value.cast一样，但是就像使用C++的dynamic_cast操作符一样工作。有关详细信息，请参阅C++参考资料。

```

```


Function: **Value.reinterpret_cast** *(type)*

> 功能：**Value.reinterpret_cast** *（类型）*


:   Like `Value.cast`, but works as if the C++ `reinterpret_cast` operator were used. Consult a C++ reference for details.

> 就像`Value.cast`一样，但是表现得就像使用C++的`reinterpret_cast`运算符一样。有关详细信息，请参阅C++参考。

```

```


Function: **Value.format_string** *(\...)*

> 功能：**Value.format_string** *(...)*


:   Convert a `gdb.Value` to a string, similarly to what the `print` command does. Invoked with no arguments, this is equivalent to calling the `str` function on the `gdb.Value`. The representation of the same value may change across different versions of [GDB], so you shouldn't, for instance, parse the strings returned by this method.

> 将`gdb.Value`转换为字符串，类似于`print`命令所做的。调用此方法无参数，相当于在`gdb.Value`上调用`str`函数。由于[GDB]的不同版本可能会改变相同值的表示，因此不应该解析此方法返回的字符串。

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

> 当设置为`False`（默认值）时，不会应用任何输出样式。
```

`summary`

:   `True` when just a summary should be printed. In this mode, scalar values are printed in their entirety, but aggregates such as structures or unions are omitted. This mode is used by `set print frame-arguments scalars` (see [Print Settings](Print-Settings.html#Print-Settings)).

```

```

```

)*


:   If this `gdb.Value` represents a string, then this method converts the contents to a Python string. Otherwise, this method will throw an exception.

> 如果这个`gdb.Value`代表一个字符串，那么这个方法就会将内容转换为Python字符串。否则，此方法将引发异常。

```

Values are interpreted as strings according to the rules of the current language. If the optional length argument is given, the string will be converted to that length, and will include any embedded zeroes that the string may contain. Otherwise, for languages where the string is zero-terminated, the entire string will be converted.

For example, in C-like languages, a value is a string if it is a pointer to or an array of characters or ints of type `wchar_t`, `char16_t`, or `char32_t`.

If the optional `encoding` is the empty string, then either the `target-charset` (see [Character Sets](Character-Sets.html#Character-Sets)) will be used, or a language-specific encoding will be used, if the current language is able to supply one.

The optional `errors` argument is the same as the corresponding argument to Python's `string.decode` method.

If the optional `length` argument is given, the string will be fetched and converted to the given length.

```

```

```

)*


:   If this `gdb.Value` represents a string, then this method converts the contents to a `gdb.LazyString` (see [Lazy Strings In Python](Lazy-Strings-In-Python.html#Lazy-Strings-In-Python)). Otherwise, this method will throw an exception.

> 如果这个`gdb.Value`代表一个字符串，那么这个方法会将内容转换为`gdb.LazyString`（参见[Python中的懒惰字符串]（Lazy-Strings-In-Python.html#Lazy-Strings-In-Python））。否则，此方法将抛出异常。

```

If the optional `encoding` will raise an error.

When a lazy string is printed, the [GDB] please see [Character Sets](Character-Sets.html#Character-Sets).

If the optional `length` argument is not provided, the string will be fetched and encoded until a null of appropriate width is found.

```

```

```


Function: **Value.fetch_lazy** *()*

> 功能：**Value.fetch_lazy** *（）*


:   If the `gdb.Value` object is currently a lazy value (`gdb.Value.is_lazy` is `True`), then the value is fetched from the inferior. Any errors that occur in the process will produce a Python exception.

> 如果`gdb.Value`对象当前是懒惰值（`gdb.Value.is_lazy`为`True`），那么该值将从下级获取。在过程中发生的任何错误都会产生一个Python异常。

```

If the `gdb.Value` object is not a lazy value, this method has no effect.

This method does not return a value.

```

---

::: header
Next: [Types In Python](Types-In-Python.html#Types-In-Python)]
:::
```
