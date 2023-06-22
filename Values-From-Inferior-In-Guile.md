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

[GDB] does not memoize `<gdb:value>` objects. `make-value` always returns a fresh object.

::: smallexample

```bash
(gdb) guile (eq? (make-value 1) (make-value 1))
$1 = #f
(gdb) guile (equal? (make-value 1) (make-value 1))
$1 = #t
```

:::

A `<gdb:value>` that represents a function can be executed via inferior function call with `value-call`. Any arguments provided to the call must match the function's prototype, and must be provided in the order specified by that prototype.

For example, `some-val` is a `<gdb:value>` instance representing a function that takes two integers as arguments. To execute this function, call it like so:

::: smallexample

```bash
(define result (value-call some-val 10 20))
```

:::

Any values returned from a function call are `<gdb:value>` objects.

Note: Unlike Python scripting in [GDB], inferior values that are simple scalars cannot be used directly in Scheme expressions that are valid for the value's data type. For example, `(+ (parse-and-eval "int_variable") 2)` does not work. And inferior values that are structures or instances of some class cannot be accessed using any special syntax, instead `value-field` must be used.

The following value-related procedures are provided by the `(gdb)` module.

Scheme Procedure: **value?** *object*

:   Return `#t` if `object` is a `<gdb:value>` object. Otherwise return `#f`.

```
<!-- -->
```

*

:   Many Scheme values can be converted directly to a `<gdb:value>` with this procedure. If `type` as described below.

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

```
<!-- -->
```

Scheme Procedure: **value-address** *value*

:   If `value` is addressable, returns a `<gdb:value>` object representing the address. Otherwise, `#f` is returned.

```
<!-- -->
```

Scheme Procedure: **value-type** *value*

:   Return the type of `value` as a `<gdb:type>` object (see [Types In Guile](Types-In-Guile.html#Types-In-Guile)).

```
<!-- -->
```

Scheme Procedure: **value-dynamic-type** *value*

:   Return the dynamic type of `value`. This uses C++ run-time type information (RTTI) to determine the dynamic type of the value. If the value is of class type, it will return the class in which the value is embedded, if any. If the value is of pointer or reference to a class type, it will compute the dynamic type of the referenced object, and return a pointer or reference to that type, respectively. In all other cases, it will return the value's static type.

```
Note that this feature will only work when debugging a C++ program that includes RTTI for the object in question. Otherwise, it will just return the static type of the value as in [ptype foo]. See [ptype](Symbols.html#Symbols).
```

```
<!-- -->
```

Scheme Procedure: **value-cast** *value type*

:   Return a new instance of `<gdb:value>` that is the result of casting `value`, which must be a `<gdb:type>` object. If the cast cannot be performed for some reason, this method throws an exception.

```
<!-- -->
```

Scheme Procedure: **value-dynamic-cast** *value type*

:   Like `value-cast`, but works as if the C++ `dynamic_cast` operator were used. Consult a C++ reference for details.

```
<!-- -->
```

Scheme Procedure: **value-reinterpret-cast** *value type*

:   Like `value-cast`, but works as if the C++ `reinterpret_cast` operator were used. Consult a C++ reference for details.

```
<!-- -->
```

Scheme Procedure: **value-dereference** *value*

:   For pointer data types, this method returns a new `<gdb:value>` object whose contents is the object pointed to by `value`. For example, if `foo` is a C pointer to an `int`, declared in your C program as

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

```

<!-- -->

```

Scheme Procedure: **value-rvalue-reference-value** *value*

:   Return a new `<gdb:value>` object which is an rvalue reference to the value encapsulated by `<gdb:value>` object `value`.

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

```

<!-- -->

```

Scheme Procedure: **value-call** *value arg-list*

:   Perform an inferior function call, taking `value` must be a \<gdb:value\> object or an object that can be converted to a value. The result is the value returned by the function.

```

<!-- -->

```

Scheme Procedure: **value-\>bool** *value*

:   Return the Scheme boolean representing `<gdb:value>` `value`. The value must be "integer like". Pointers are ok.

```

<!-- -->

```

Scheme Procedure: **value-\>integer**

:   Return the Scheme integer representing `<gdb:value>` `value`. The value must be "integer like". Pointers are ok.

```

<!-- -->

```

Scheme Procedure: **value-\>real**

:   Return the Scheme real number representing `<gdb:value>` `value`. The value must be a number.

```

<!-- -->

```

Scheme Procedure: **value-\>bytevector**

:   Return a Scheme bytevector with the raw contents of `<gdb:value>` `value`. No transformation, endian or otherwise, is performed.

```

<!-- -->

```

*

:   If `value>` represents a string, then this method converts the contents to a Guile string. Otherwise, this method will throw an exception.

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

```

<!-- -->

```

Scheme Procedure: **value-fetch-lazy!** *value*

:   If `value` is a lazy value (`(value-lazy? value)` is `#t`), then the value is fetched from the inferior. Any errors that occur in the process will produce a Guile exception.

```

If `value` is not a lazy value, this method has no effect.

The result of this function is unspecified.

```

```

<!-- -->

```

Scheme Procedure: **value-print** *value*

:   Return the string representation (print form) of `<gdb:value>` `value`.

---

::: header
Next: [Arithmetic In Guile](Arithmetic-In-Guile.html#Arithmetic-In-Guile)]
:::
```
