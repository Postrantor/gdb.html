---
description: Types In Guile (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Types In Guile (Debugging with GDB)
lang: en
resource-type: document
title: Types In Guile (Debugging with GDB)
---
::: header
Next: [Guile Pretty Printing API](Guile-Pretty-Printing-API.html#Guile-Pretty-Printing-API)]
:::

---

#### 23.4.3.7 Types In Guile

[GDB] represents types from the inferior in objects of type `<gdb:type>`.

The following type-related procedures are provided by the `(gdb)` module.

Scheme Procedure: **type?** *object*

:   Return `#t` if `object` is an object of type `<gdb:type>`. Otherwise return `#f`.

```
<!-- -->
```

*

:   This function looks up a type by its `name`, which must be a string.

```
If `block` is looked up in that scope. Otherwise, it is searched for globally.

Ordinarily, this function will return an instance of `<gdb:type>`. If the named type cannot be found, it will throw an exception.
```

```
<!-- -->
```

Scheme Procedure: **type-code** *type*

:   Return the type code of `type`. The type code will be one of the `TYPE_CODE_` constants defined below.

```
<!-- -->
```

Scheme Procedure: **type-tag** *type*

:   Return the tag name of `type`. The tag name is the name after `struct`, `union`, or `enum` in C and C++; not all languages have this concept. If this type has no tag name, then `#f` is returned.

```
<!-- -->
```

Scheme Procedure: **type-name** *type*

:   Return the name of `type`. If this type has no name, then `#f` is returned.

```
<!-- -->
```

Scheme Procedure: **type-print-name** *type*

:   Return the print name of `type`"` is returned.

```
<!-- -->
```

Scheme Procedure: **type-sizeof** *type*

:   Return the size of this type, in target `char` units. Usually, a target's `char` type will be an 8-bit byte. However, on some unusual platforms, this type may have a different size.

```
<!-- -->
```

Scheme Procedure: **type-strip-typedefs** *type*

:   Return a new `<gdb:type>` that represents the real type of `type`, after removing all layers of typedefs.

```
<!-- -->
```

*

:   Return a new `<gdb:type>` object which represents an array of this type. If one argument is given, it is the inclusive upper bound of the array; in this case the lower bound is zero. If two arguments are given, the first argument is the lower bound of the array, and the second argument is the upper bound of the array. An array's length must not be negative, but the bounds can be.

```
<!-- -->
```

*

:   Return a new `<gdb:type>` object which represents a vector of this type. If one argument is given, it is the inclusive upper bound of the vector; in this case the lower bound is zero. If two arguments are given, the first argument is the lower bound of the vector, and the second argument is the upper bound of the vector. A vector's length must not be negative, but the bounds can be.

```
The difference between an `array` and a `vector` is that arrays behave like in C: when used in expressions they decay to a pointer to the first element whereas vectors are treated as first class values.
```

```
<!-- -->
```

Scheme Procedure: **type-pointer** *type*

:   Return a new `<gdb:type>` object which represents a pointer to `type`.

```
<!-- -->
```

Scheme Procedure: **type-range** *type*

:   Return a list of two elements: the low bound and high bound of `type` does not have a range, an exception is thrown.

```
<!-- -->
```

Scheme Procedure: **type-reference** *type*

:   Return a new `<gdb:type>` object which represents a reference to `type`.

```
<!-- -->
```

Scheme Procedure: **type-target** *type*

:   Return a new `<gdb:type>` object which represents the target type of `type`.

```
For a pointer type, the target type is the type of the pointed-to object. For an array type (meaning C-like arrays), the target type is the type of the elements of the array. For a function or method type, the target type is the type of the return value. For a complex type, the target type is the type of the elements. For a typedef, the target type is the aliased type.

If the type does not have a target, this method will throw an exception.
```

```
<!-- -->
```

Scheme Procedure: **type-const** *type*

:   Return a new `<gdb:type>` object which represents a `const`-qualified variant of `type`.

```
<!-- -->
```

Scheme Procedure: **type-volatile** *type*

:   Return a new `<gdb:type>` object which represents a `volatile`-qualified variant of `type`.

```
<!-- -->
```

Scheme Procedure: **type-unqualified** *type*

:   Return a new `<gdb:type>` object which represents an unqualified variant of `type`. That is, the result is neither `const` nor `volatile`.

```
<!-- -->
```

Scheme Procedure: **type-num-fields**

:   Return the number of fields of `<gdb:type>` `type`.

```
<!-- -->
```

Scheme Procedure: **type-fields** *type*

:   Return the fields of `type` as a list. For structure and union types, `fields` has the usual meaning. Range types have two fields, the minimum and maximum values. Enum types have one field per enum constant. Function and method types have one field per parameter. The base types of C++ classes are also represented as fields. If the type has no fields, or does not fit into one of these categories, an empty list will be returned. See [Fields of a type in Guile](#Fields-of-a-type-in-Guile).

```
<!-- -->
```

Scheme Procedure: **make-field-iterator** *type*

:   Return the fields of `type` as a \<gdb:iterator\> object. See [Iterators In Guile](Iterators-In-Guile.html#Iterators-In-Guile).

```
<!-- -->
```

Scheme Procedure: **type-field** *type field-name*

:   Return field named `field-name`, an exception is thrown.

```
For example, if `some-type` is a `<gdb:type>` instance holding a structure type, you can access its `foo` field with:

::: smallexample
``` smallexample
(define bar (type-field some-type "foo"))
```

:::

`bar` will be a `<gdb:field>` object.

```

```

<!-- -->

```

Scheme Procedure: **type-has-field?** *type name*

:   Return `#t` if `<gdb:type>` `type`. Otherwise return `#f`.

Each type has a code, which indicates what category this type falls into. The available type categories are represented by constants defined in the `(gdb)` module:

`TYPE_CODE_PTR` 

:   The type is a pointer.

`TYPE_CODE_ARRAY` 

:   The type is an array.

`TYPE_CODE_STRUCT` 

:   The type is a structure.

`TYPE_CODE_UNION` 

:   The type is a union.

`TYPE_CODE_ENUM` 

:   The type is an enum.

`TYPE_CODE_FLAGS` 

:   A bit flags type, used for things such as status registers.

`TYPE_CODE_FUNC` 

:   The type is a function.

`TYPE_CODE_INT` 

:   The type is an integer type.

`TYPE_CODE_FLT` 

:   A floating point type.

`TYPE_CODE_VOID` 

:   The special type `void`.

`TYPE_CODE_SET` 

:   A Pascal set type.

`TYPE_CODE_RANGE` 

:   A range type, that is, an integer type with bounds.

`TYPE_CODE_STRING` 

:   A string type. Note that this is only used for certain languages with language-defined string types; C strings are not represented this way.

`TYPE_CODE_BITSTRING` 

:   A string of bits. It is deprecated.

`TYPE_CODE_ERROR` 

:   An unknown or erroneous type.

`TYPE_CODE_METHOD` 

:   A method type, as found in C++.

`TYPE_CODE_METHODPTR` 

:   A pointer-to-member-function.

`TYPE_CODE_MEMBERPTR` 

:   A pointer-to-member.

`TYPE_CODE_REF` 

:   A reference type.

`TYPE_CODE_RVALUE_REF` 

:   A C++11 rvalue reference type.

`TYPE_CODE_CHAR` 

:   A character type.

`TYPE_CODE_BOOL` 

:   A boolean type.

`TYPE_CODE_COMPLEX` 

:   A complex float type.

`TYPE_CODE_TYPEDEF` 

:   A typedef to some other type.

`TYPE_CODE_NAMESPACE` 

:   A C++ namespace.

`TYPE_CODE_DECFLOAT` 

:   A decimal floating point type.

`TYPE_CODE_INTERNAL_FUNCTION` 

:   A function internal to [GDB]. This is the type used to represent convenience functions (see [Convenience Funs](Convenience-Funs.html#Convenience-Funs)).

```

```

`gdb.TYPE_CODE_XMETHOD` 

:   A method internal to [GDB]. This is the type used to represent xmethods (see [Writing an Xmethod](Writing-an-Xmethod.html#Writing-an-Xmethod)).

```

```

`gdb.TYPE_CODE_FIXED_POINT` 

:   A fixed-point number.

```

```

`gdb.TYPE_CODE_NAMESPACE` 

:   A Fortran namelist.

Further support for types is provided in the `(gdb types)` Guile module (see [Guile Types Module](Guile-Types-Module.html#Guile-Types-Module)).



Each field is represented as an object of type `<gdb:field>`.

The following field-related procedures are provided by the `(gdb)` module:

Scheme Procedure: **field?** *object*

:   Return `#t` if `object` is an object of type `<gdb:field>`. Otherwise return `#f`.

```

<!-- -->

```

Scheme Procedure: **field-name** *field*

:   Return the name of the field, or `#f` for anonymous fields.

```

<!-- -->

```

Scheme Procedure: **field-type** *field*

:   Return the type of the field. This is usually an instance of `<gdb:type>`, but it can be `#f` in some situations.

```

<!-- -->

```

Scheme Procedure: **field-enumval** *field*

:   Return the enum value represented by `<gdb:field>` `field`.

```

<!-- -->

```

Scheme Procedure: **field-bitpos** *field*

:   Return the bit position of `<gdb:field>` `field`. This attribute is not available for `static` fields (as in C++).

```

<!-- -->

```

Scheme Procedure: **field-bitsize** *field*

:   If the field is packed, or is a bitfield, return the size of `<gdb:field>` `field` in bits. Otherwise, zero is returned; in which case the field's size is given by its type.

```

<!-- -->

```

Scheme Procedure: **field-artificial?** *field*

:   Return `#t` if the field is artificial, usually meaning that it was provided by the compiler and not the user. Otherwise return `#f`.

```

<!-- -->

```

Scheme Procedure: **field-base-class?** *field*

:   Return `#t` if the field represents a base class of a C++ structure. Otherwise return `#f`.

---

::: header
Next: [Guile Pretty Printing API](Guile-Pretty-Printing-API.html#Guile-Pretty-Printing-API)]
:::
```
