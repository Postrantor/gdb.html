---
tip: translate by openai@2023-06-24 04:35:12
...
---
description: Values From Inferior In Guile (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Values From Inferior In Guile (Debugging with GDB)
lang: en
resource-type: document
title: Values From Inferior In Guile (Debugging with GDB)
---
::: header
Next: [Arithmetic In Guile](Arithmetic-In-Guile.html#Arithmetic-In-Guile)]
:::

---

#### 23.4.3.5 Values From Inferior In Guile


[GDB] uses this object for its internal bookkeeping of the inferior's values, and for fetching values when necessary.

> [GDB]使用此对象来进行内部的下级值簿记，并在必要时获取值。


[GDB] does not memoize `<gdb:value>` objects. `make-value` always returns a fresh object.

> GDB不会记忆<gdb:value>对象。make-value总是会返回一个新的对象。

::: smallexample

```bash
(gdb) guile (eq? (make-value 1) (make-value 1))
$1 = #f
(gdb) guile (equal? (make-value 1) (make-value 1))
$1 = #t
```

:::


A `<gdb:value>` that represents a function can be executed via inferior function call with `value-call`. Any arguments provided to the call must match the function's prototype, and must be provided in the order specified by that prototype.

> 一个`<gdb:value>`代表的函数可以通过inferior function call使用`value-call`来执行。提供给调用的任何参数都必须与函数的原型匹配，并且必须按照该原型指定的顺序提供。


For example, `some-val` is a `<gdb:value>` instance representing a function that takes two integers as arguments. To execute this function, call it like so:

> 例如，`some-val`是一个`<gdb:value>`实例，代表一个接受两个整数参数的函数。要执行此函数，请按如下方式调用它：

::: smallexample

```bash
(define result (value-call some-val 10 20))
```

:::

Any values returned from a function call are `<gdb:value>` objects.


Note: Unlike Python scripting in [GDB], inferior values that are simple scalars cannot be used directly in Scheme expressions that are valid for the value's data type. For example, `(+ (parse-and-eval "int_variable") 2)` does not work. And inferior values that are structures or instances of some class cannot be accessed using any special syntax, instead `value-field` must be used.

> 注意：与在[GDB]中使用Python脚本不同，简单标量的下级值不能直接用于值的数据类型的Scheme表达式中。例如，`(+ (parse-and-eval "int_variable") 2)`不起作用。结构或某个类的实例的下级值不能使用任何特殊语法访问，而必须使用`value-field`。


The following value-related procedures are provided by the `(gdb)` module.

> 以下和值有关的程序由(gdb)模块提供。

Scheme Procedure: **value?** *object*


:   Return `#t` if `object` is a `<gdb:value>` object. Otherwise return `#f`.

> 如果对象是一个<gdb:value>对象，则返回#t。否则返回#f。

```
<!-- -->
```

*


:   Many Scheme values can be converted directly to a `<gdb:value>` with this procedure. If `type` as described below.

> 許多Scheme值可以通過該程序直接轉換為<gdb:value>。如下所述，請指定類型。

```
See [Architectures In Guile](Architectures-In-Guile.html#Architectures-In-Guile), for a list of the builtin types for an architecture.

Here's how Scheme values are converted when `type` argument to `make-value` is not specified:

Scheme boolean

:   A Scheme boolean is converted the boolean type for the current language.

Scheme integer

:   A Scheme integer is converted to the first of a C `int`, `unsigned int`, `long`, `unsigned long`, `long long` or `unsigned long long` type for the current architecture that can represent the value.

    If the Scheme integer cannot be represented as a target integer an `out-of-range` exception is thrown.

Scheme real

:   A Scheme real is converted to the C `double` type for the current architecture.

Scheme string

:   A Scheme string is converted to a string in the current target language using the current target encoding. Characters that cannot be represented in the current target encoding are replaced with the corresponding escape sequence. This is Guile's `SCM_FAILED_CONVERSION_ESCAPE_SEQUENCE` conversion strategy (see [Strings](http://www.gnu.org/software/guile/manual/html_node/Strings.html#Strings) in GNU Guile Reference Manual).

    Passing `type` is not supported in this case, if it is provided a `wrong-type-arg` exception is thrown.

`<gdb:lazy-string>`

:   If `value` is a `<gdb:lazy-string>` object (see [Lazy Strings In Guile](Lazy-Strings-In-Guile.html#Lazy-Strings-In-Guile)), then the `lazy-string->value` procedure is called, and its result is used.

    Passing `type` is not supported in this case, if it is provided a `wrong-type-arg` exception is thrown.

Scheme bytevector

:   If `value`, and the result is essentially created by using `memcpy`.

    If `value` is not provided, the result is an array of type `uint8` of the same length.
```

Scheme Procedure: **value-optimized-out?** *value*


:   Return `#t` if the compiler optimized out `value`, thus it is not available for fetching from the inferior. Otherwise return `#f`.

> 如果编译器优化了`value`，则返回`#t`，因此无法从低级别获取它。否则返回`#f`。

```
<!-- -->
```

Scheme Procedure: **value-address** *value*


:   If `value` is addressable, returns a `<gdb:value>` object representing the address. Otherwise, `#f` is returned.

> 如果`value`是可寻址的，则返回一个代表地址的`<gdb:value>`对象。否则，返回`#f`。

```
<!-- -->
```

Scheme Procedure: **value-type** *value*


:   Return the type of `value` as a `<gdb:type>` object (see [Types In Guile](Types-In-Guile.html#Types-In-Guile)).

> 返回`value`的类型作为`<gdb:type>`对象（参见[Guile中的类型](Types-In-Guile.html#Types-In-Guile)）。

```
<!-- -->
```

Scheme Procedure: **value-dynamic-type** *value*


:   Return the dynamic type of `value`. This uses C++ run-time type information (RTTI) to determine the dynamic type of the value. If the value is of class type, it will return the class in which the value is embedded, if any. If the value is of pointer or reference to a class type, it will compute the dynamic type of the referenced object, and return a pointer or reference to that type, respectively. In all other cases, it will return the value's static type.

> 返回`value`的动态类型。这使用C++运行时类型信息（RTTI）来确定值的动态类型。如果值是类类型，它将返回值嵌入的类（如果有的话）。如果值是指向类类型的指针或引用，它将计算引用对象的动态类型，并分别返回指向该类型的指针或引用。在所有其他情况下，它将返回值的静态类型。

```
Note that this feature will only work when debugging a C++ program that includes RTTI for the object in question. Otherwise, it will just return the static type of the value as in [ptype foo]. See [ptype](Symbols.html#Symbols).
```

```
<!-- -->
```

Scheme Procedure: **value-cast** *value type*


:   Return a new instance of `<gdb:value>` that is the result of casting `value`, which must be a `<gdb:type>` object. If the cast cannot be performed for some reason, this method throws an exception.

> 返回一个新的<gdb:value>实例，该实例是对value（必须是<gdb:type>对象）执行类型转换的结果。如果由于某种原因无法执行转换，此方法将抛出异常。

```
<!-- -->
```

Scheme Procedure: **value-dynamic-cast** *value type*


:   Like `value-cast`, but works as if the C++ `dynamic_cast` operator were used. Consult a C++ reference for details.

> 就像"value-cast"一样，但是像使用C++的"dynamic_cast"操作符一样工作。有关详细信息，请参阅C++参考文档。

```
<!-- -->
```

Scheme Procedure: **value-reinterpret-cast** *value type*


:   Like `value-cast`, but works as if the C++ `reinterpret_cast` operator were used. Consult a C++ reference for details.

> 像“value-cast”一样，但是就像使用C++的“reinterpret_cast”操作符一样工作。有关详细信息，请参阅C++参考。

```
<!-- -->
```

Scheme Procedure: **value-dereference** *value*


:   For pointer data types, this method returns a new `<gdb:value>` object whose contents is the object pointed to by `value`. For example, if `foo` is a C pointer to an `int`, declared in your C program as

> 对于指针数据类型，此方法返回一个新的`<gdb:value>`对象，其内容是由`value`指向的对象。例如，如果在您的C程序中声明`foo`是一个指向`int`的C指针，

```
::: smallexample
``` smallexample
int *foo;
```

:::

then you can use the corresponding `<gdb:value>` to access what `foo` points to like this:

::: smallexample

```bash
(define bar (value-dereference foo))
```

:::

The result `bar` will be a `<gdb:value>` object holding the value pointed to by `foo`.

A similar function `value-referenced-value` exists which also returns `<gdb:value>` objects corresponding to the values pointed to by pointer values (and additionally, values referenced by reference values). However, the behavior of `value-dereference` differs from `value-referenced-value` by the fact that the behavior of `value-dereference` is identical to applying the C unary operator `*` on a given value. For example, consider a reference to a pointer `ptrref`, declared in your C++ program as

::: smallexample

```bash
typedef int *intptr;
...
int val = 10;
intptr ptr = &val;
intptr &ptrref = ptr;
```

:::

Though `ptrref` is a reference value, one can apply the method `value-dereference` to the `<gdb:value>` object corresponding to it and obtain a `<gdb:value>` which is identical to that corresponding to `val`. However, if you apply the method `value-referenced-value`, the result would be a `<gdb:value>` object identical to that corresponding to `ptr`.

::: smallexample

```bash
(define scm-ptrref (parse-and-eval "ptrref"))
(define scm-val (value-dereference scm-ptrref))
(define scm-ptr (value-referenced-value scm-ptrref))
```

:::

The `<gdb:value>` object `scm-val` is identical to that corresponding to `val`, and `scm-ptr` is identical to that corresponding to `ptr`. In general, `value-dereference` can be applied whenever the C unary operator `*` can be applied to the corresponding C value. For those cases where applying both `value-dereference` and `value-referenced-value` is allowed, the results obtained need not be identical (as we have seen in the above example). The results are however identical when applied on `<gdb:value>` objects corresponding to pointers (`<gdb:value>` objects with type code `TYPE_CODE_PTR`) in a C/C++ program.

```

```

<!-- -->

```

Scheme Procedure: **value-referenced-value** *value*


:   For pointer or reference data types, this method returns a new `<gdb:value>` object corresponding to the value referenced by the pointer/reference value. For pointer data types, `value-dereference` and `value-referenced-value` produce identical results. The difference between these methods is that `value-dereference` cannot get the values referenced by reference values. For example, consider a reference to an `int`, declared in your C++ program as

> 对于指针或引用数据类型，此方法返回一个新的`<gdb:value>`对象，该对象对应于指针/引用值引用的值。对于指针数据类型，`value-dereference`和`value-referenced-value`产生相同的结果。这些方法之间的区别在于，`value-dereference`无法获取引用值引用的值。例如，在您的C ++程序中声明一个`int`的引用，

```

::: smallexample

```bash
int val = 10;
int &ref = val;
```

:::

then applying `value-dereference` to the `<gdb:value>` object corresponding to `ref` will result in an error, while applying `value-referenced-value` will result in a `<gdb:value>` object identical to that corresponding to `val`.

::: smallexample

```bash
(define scm-ref (parse-and-eval "ref"))
(define err-ref (value-dereference scm-ref))      ;; error
(define scm-val (value-referenced-value scm-ref)) ;; ok
```

:::

The `<gdb:value>` object `scm-val` is identical to that corresponding to `val`.

```

```

<!-- -->

```

Scheme Procedure: **value-reference-value** *value*


:   Return a new `<gdb:value>` object which is a reference to the value encapsulated by `<gdb:value>` object `value`.

> 返回一个新的<gdb:value>对象，该对象是对由<gdb:value>对象value封装的值的引用。

```

<!-- -->

```

Scheme Procedure: **value-rvalue-reference-value** *value*


:   Return a new `<gdb:value>` object which is an rvalue reference to the value encapsulated by `<gdb:value>` object `value`.

> 返回一个新的`<gdb:value>`对象，它是`<gdb:value>`对象`value`所封装值的右值引用。

```

<!-- -->

```

Scheme Procedure: **value-const-value** *value*

:   Return a new `<gdb:value>` object which is a '`const`.

```

<!-- -->

```

Scheme Procedure: **value-field** *value field-name*

:   Return field `field-name`.

```

<!-- -->

```

Scheme Procedure: **value-subscript** *value index*


:   Return the value of array `value` argument must be a subscriptable `<gdb:value>` object.

> 返回数组的值，`value`参数必须是可访问的<gdb:value>对象。

```

<!-- -->

```

Scheme Procedure: **value-call** *value arg-list*


:   Perform an inferior function call, taking `value` must be a \<gdb:value\> object or an object that can be converted to a value. The result is the value returned by the function.

> 执行一个次级函数调用，`value`必须是一个\<gdb:value\>对象或可以转换为值的对象。结果是函数返回的值。

```

<!-- -->

```

Scheme Procedure: **value-\>bool** *value*


:   Return the Scheme boolean representing `<gdb:value>` `value`. The value must be "integer like". Pointers are ok.

> 返回表示`<gdb:value>` `value`的Scheme布尔值。该值必须是“类似整数”的。指针也可以。

```

<!-- -->

```

Scheme Procedure: **value-\>integer**


:   Return the Scheme integer representing `<gdb:value>` `value`. The value must be "integer like". Pointers are ok.

> 返回代表<gdb:value>值的Scheme整数。该值必须是“类似整数”的。指针也可以。

```

<!-- -->

```

Scheme Procedure: **value-\>real**


:   Return the Scheme real number representing `<gdb:value>` `value`. The value must be a number.

> 返回表示'<gdb:value>' 'value'的Scheme实数。该值必须是一个数字。

```

<!-- -->

```

Scheme Procedure: **value-\>bytevector**


:   Return a Scheme bytevector with the raw contents of `<gdb:value>` `value`. No transformation, endian or otherwise, is performed.

> 返回一个Scheme字节向量，其中包含`<gdb:value>` `value`的原始内容。不会执行任何转换或字节序转换。

```

<!-- -->

```

*


:   If `value>` represents a string, then this method converts the contents to a Guile string. Otherwise, this method will throw an exception.

> 如果`value>`代表一个字符串，那么这个方法将内容转换为Guile字符串。否则，此方法将抛出异常。

```

Values are interpreted as strings according to the rules of the current language. If the optional length argument is given, the string will be converted to that length, and will include any embedded zeroes that the string may contain. Otherwise, for languages where the string is zero-terminated, the entire string will be converted.

For example, in C-like languages, a value is a string if it is a pointer to or an array of characters or ints of type `wchar_t`, `char16_t`, or `char32_t`.

If the optional `encoding` is the empty string, then either the `target-charset` (see [Character Sets](Character-Sets.html#Character-Sets)) will be used, or a language-specific encoding will be used, if the current language is able to supply one.

The optional `errors` is not specified, or if its value is `#f`, then the default conversion strategy is used, which is set with the Scheme function `set-port-conversion-strategy!`. If the value is `'error` then an exception is thrown if there is any conversion error. If the value is `'substitute` then any conversion error is replaced with question marks. See [Strings](http://www.gnu.org/software/guile/manual/html_node/Strings.html#Strings) in GNU Guile Reference Manual.

If the optional `length` argument is given, the string will be fetched and converted to the given length. The length must be a Scheme integer and not a `<gdb:value>` integer.

```

```

<!-- -->

```

*


:   If this `<gdb:value>` represents a string, then this method converts `value` to a `<gdb:lazy-string` (see [Lazy Strings In Guile](Lazy-Strings-In-Guile.html#Lazy-Strings-In-Guile)). Otherwise, this method will throw an exception.

> 如果这个`<gdb:value>`代表一个字符串，那么这个方法将把`value`转换为`<gdb:lazy-string`（参见[Guile中的懒惰字符串](Lazy-Strings-In-Guile.html#Lazy-Strings-In-Guile)）。否则，此方法将抛出异常。

```

If the optional `encoding` will raise an error.

When a lazy string is printed, the [GDB] please see [Character Sets](Character-Sets.html#Character-Sets).

If the optional `length` argument is not provided, the string will be fetched and encoded until a null of appropriate width is found. The length must be a Scheme integer and not a `<gdb:value>` integer.

```

```

<!-- -->

```

Scheme Procedure: **value-lazy?** *value*


:   Return `#t` if `value` does not fetch values until necessary, for efficiency. For example:

> 如果`值`为了提高效率而不必要地取回值，则返回`#t`。例如：

```

::: smallexample

```bash
(define myval (parse-and-eval "somevar"))
```

:::

The value of `somevar` is not fetched at this time. It will be fetched when the value is needed, or when the `fetch-lazy` procedure is invoked.

```

```

<!-- -->

```

Scheme Procedure: **make-lazy-value** *type address*


:   Return a `<gdb:value>` that will be lazily fetched from the target. The object of type `<gdb:type>` whose value to fetch is specified by its `type`, which is a Scheme integer.

> 返回一个惰性从目标获取的`<gdb:value>`。要获取的类型为`<gdb:type>`的对象的值由其类型指定，该类型是一个Scheme整数。

```

<!-- -->

```

Scheme Procedure: **value-fetch-lazy!** *value*


:   If `value` is a lazy value (`(value-lazy? value)` is `#t`), then the value is fetched from the inferior. Any errors that occur in the process will produce a Guile exception.

> 如果`value`是一个懒惰值（`(value-lazy? value)`是`#t`），那么会从下属处获取该值。过程中发生的任何错误都会引发Guile异常。

```

If `value` is not a lazy value, this method has no effect.

The result of this function is unspecified.

```

```

<!-- -->

```

Scheme Procedure: **value-print** *value*


:   Return the string representation (print form) of `<gdb:value>` `value`.

> 返回<gdb:value>值的字符串表示（打印形式）。

---

::: header
Next: [Arithmetic In Guile](Arithmetic-In-Guile.html#Arithmetic-In-Guile)]
:::
```
