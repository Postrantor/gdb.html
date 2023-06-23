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

Inferior values that are simple scalars can be used directly in Python expressions that are valid for the value's data type. Here's an example for an integer or floating-point value `some_val`:

::: smallexample

```bash
bar = some_val + 2
```

:::

As result of this, `bar` will also be a `gdb.Value` object whose values are of the same type as those of `some_val`. Valid Python operations can also be performed on `gdb.Value` objects representing a `struct` or `class` object. For such cases, the overloaded operator (if present), is used to perform the operation. For example, if `val1` and `val2` are `gdb.Value` objects representing instances of a `class` which overloads the `+` operator, then one can use the `+` operator in their Python script as follows:

::: smallexample

```bash
val3 = val1 + val2
```

:::

The result of the operation `val3` is also a `gdb.Value` object corresponding to the value returned by the overloaded `+` operator. In general, overloaded operators are invoked for the following operations: `+` (binary addition), `-` (binary subtraction), `*` (multiplication), `/`, `%`, `<<`, `>>`, `|`, `&`, `^`.

Inferior values that are structures or instances of some class can be accessed using the Python *dictionary syntax*. For example, if `some_val` is a `gdb.Value` instance holding a structure, you can access its `foo` element with:

::: smallexample

```bash
bar = some_val['foo']
```

:::

Again, `bar` will also be a `gdb.Value` object. Structure elements can also be accessed by using `gdb.Field` objects as subscripts (see [Types In Python](Types-In-Python.html#Types-In-Python), for more information on `gdb.Field` objects). For example, if `foo_field` is a `gdb.Field` object corresponding to element `foo` of the above structure, then `bar` can also be accessed as follows:

::: smallexample

```bash
bar = some_val[foo_field]
```

:::

A `gdb.Value` that represents a function can be executed via inferior function call. Any arguments provided to the call must match the function's prototype, and must be provided in the order specified by that prototype.

For example, `some_val` is a `gdb.Value` instance representing a function that takes two integers as arguments. To execute this function, call it like so:

::: smallexample

```bash
result = some_val (10,20)
```

:::

Any values returned from a function call will be stored as a `gdb.Value`.

The following attributes are provided:

Variable: **Value.address**

:   If this object is addressable, this read-only attribute holds a `gdb.Value` object representing the address. Otherwise, this attribute holds `None`.

Variable: **Value.is_optimized_out**

:   This read-only boolean attribute is true if the compiler optimized out this value, thus it is not available for fetching from the inferior.

```
<!-- -->
```

Variable: **Value.type**

:   The type of this `gdb.Value`. The value of this attribute is a `gdb.Type` object (see [Types In Python](Types-In-Python.html#Types-In-Python)).

```
<!-- -->
```

Variable: **Value.dynamic_type**

:   The dynamic type of this `gdb.Value`. This uses the object's virtual table and the C++ run-time type information (RTTI) to determine the dynamic type of the value. If this value is of class type, it will return the class in which the value is embedded, if any. If this value is of pointer or reference to a class type, it will compute the dynamic type of the referenced object, and return a pointer or reference to that type, respectively. In all other cases, it will return the value's static type.

```
Note that this feature will only work when debugging a C++ program that includes RTTI for the object in question. Otherwise, it will just return the static type of the value as in [ptype foo] (see [ptype](Symbols.html#Symbols)).
```

```
<!-- -->
```

Variable: **Value.is_lazy**

:   The value of this read-only boolean attribute is `True` if this `gdb.Value` has not yet been fetched from the inferior. [GDB] does not fetch values until necessary, for efficiency. For example:

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

```

If `type` was not passed at all.

```

```

<!-- -->

```

Function: **Value.assign** *(rhs)*

:   Assign `rhs` to this value, and return `None`. If this value cannot be assigned to, or if the assignment is invalid for some reason (for example a type-checking failure), an exception will be thrown.

```

<!-- -->

```

Function: **Value.cast** *(type)*

:   Return a new instance of `gdb.Value` that is the result of casting this instance to the type described by `type`, which must be a `gdb.Type` object. If the cast cannot be performed for some reason, this method throws an exception.

```

<!-- -->

```

Function: **Value.dereference** *()*

:   For pointer data types, this method returns a new `gdb.Value` object whose contents is the object pointed to by the pointer. For example, if `foo` is a C pointer to an `int`, declared in your C program as

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

```

<!-- -->

```

Function: **Value.const_value** *()*

:   Return a `gdb.Value` object which is a `const` version of the value encapsulated by this instance.

```

<!-- -->

```

Function: **Value.dynamic_cast** *(type)*

:   Like `Value.cast`, but works as if the C++ `dynamic_cast` operator were used. Consult a C++ reference for details.

```

<!-- -->

```

Function: **Value.reinterpret_cast** *(type)*

:   Like `Value.cast`, but works as if the C++ `reinterpret_cast` operator were used. Consult a C++ reference for details.

```

<!-- -->

```

Function: **Value.format_string** *(\...)*

:   Convert a `gdb.Value` to a string, similarly to what the `print` command does. Invoked with no arguments, this is equivalent to calling the `str` function on the `gdb.Value`. The representation of the same value may change across different versions of [GDB], so you shouldn't, for instance, parse the strings returned by this method.

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

```

If the `gdb.Value` object is not a lazy value, this method has no effect.

This method does not return a value.

```

---

::: header
Next: [Types In Python](Types-In-Python.html#Types-In-Python)]
:::
```
