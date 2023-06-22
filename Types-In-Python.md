---
description: Types In Python (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Types In Python (Debugging with GDB)
lang: en
resource-type: document
title: Types In Python (Debugging with GDB)
---
::: header
Next: [Pretty Printing API](Pretty-Printing-API.html#Pretty-Printing-API)]
:::

---

#### 23.3.2.4 Types In Python

[GDB] represents types from the inferior using the class `gdb.Type`.

The following type-related functions are available in the `gdb` module:

)*

:   This function looks up a type by its `name`, which must be a string.

```
If `block` is looked up in that scope. Otherwise, it is searched for globally.

Ordinarily, this function will return an instance of `gdb.Type`. If the named type cannot be found, it will throw an exception.
```

Integer types can be found without looking them up by name. See [Architectures In Python](Architectures-In-Python.html#Architectures-In-Python), for the `integer_type` method.

If the type is a structure or class type, or an enum type, the fields of that type can be accessed using the Python *dictionary syntax*. For example, if `some_type` is a `gdb.Type` instance holding a structure type, you can access its `foo` field with:

::: smallexample

```bash
bar = some_type['foo']
```

:::

`bar` will be a `gdb.Field` object; see below under the description of the `Type.fields` method for a description of the `gdb.Field` class.

An instance of `Type` has the following attributes:

Variable: **Type.alignof**

:   The alignment of this type, in bytes. Type alignment comes from the debugging information; if it was not specified, then [GDB] will use the relevant ABI to try to determine the alignment. In some cases, even this is not possible, and zero will be returned.

```
<!-- -->
```

Variable: **Type.code**

:   The type code for this type. The type code will be one of the `TYPE_CODE_` constants defined below.

```
<!-- -->
```

Variable: **Type.dynamic**

:   A boolean indicating whether this type is dynamic. In some situations, such as Rust `enum` types or Ada variant records, the concrete type of a value may vary depending on its contents. That is, the declared type of a variable, or the type returned by `gdb.lookup_type` may be dynamic; while the type of the variable's value will be a concrete instance of that dynamic type.

```
For example, consider this code:

::: smallexample
``` smallexample
int n;
int array[n];
```

:::

Here, at least conceptually (whether your compiler actually does this is a separate issue), examining `gdb.lookup_symbol("array", ...).type` could yield a `gdb.Type` which reports a size of `None`. This is the dynamic type.

However, examining `gdb.parse_and_eval("array").type` would yield a concrete type, whose length would be known.

```

```

<!-- -->

```

Variable: **Type.name**

:   The name of this type. If this type has no name, then `None` is returned.

```

<!-- -->

```

Variable: **Type.sizeof**

:   The size of this type, in target `char` units. Usually, a target's `char` type will be an 8-bit byte. However, on some unusual platforms, this type may have a different size. A dynamic type may not have a fixed size; in this case, this attribute's value will be `None`.

```

<!-- -->

```

Variable: **Type.tag**

:   The tag name for this type. The tag name is the name after `struct`, `union`, or `enum` in C and C++; not all languages have this concept. If this type has no tag name, then `None` is returned.

```

<!-- -->

```

Variable: **Type.objfile**

:   The `gdb.Objfile` that this type was defined in, or `None` if there is no associated objfile.

```

<!-- -->

```

Variable: **Type.is_scalar**

:   This property is `True` if the type is a scalar type, otherwise, this property is `False`. Examples of non-scalar types include structures, unions, and classes.

```

<!-- -->

```

Variable: **Type.is_signed**

:   For scalar types (those for which `Type.is_scalar` is `True`), this property is `True` if the type is signed, otherwise this property is `False`.

```

Attempting to read this property for a non-scalar type (a type for which `Type.is_scalar` is `False`), will raise a `ValueError`.

```

The following methods are provided:

Function: **Type.fields** *()*

:   Return the fields of this type. The behavior depends on the type code:

```

- For structure and union types, this method returns the fields.
- Range types have two fields, the minimum and maximum values.
- Enum types have one field per enum constant.
- Function and method types have one field per parameter. The base types of C++ classes are also represented as fields.
- Array types have one field representing the array's range.
- If the type does not fit into one of these categories, a `TypeError` is raised.

Each field is a `gdb.Field` object, with some pre-defined attributes:

`bitpos`

:   This attribute is not available for `enum` or `static` (as in C++) fields. The value is the position, counting in bits, from the start of the containing type. Note that, in a dynamic type, the position of a field may not be constant. In this case, the value will be `None`. Also, a dynamic type may have fields that do not appear in a corresponding concrete type.

`enumval`

:   This attribute is only available for `enum` fields, and its value is the enumeration member's integer representation.

`name`

:   The name of the field, or `None` for anonymous fields.

`artificial`

:   This is `True` if the field is artificial, usually meaning that it was provided by the compiler and not the user. This attribute is always provided, and is `False` if the field is not artificial.

`is_base_class`

:   This is `True` if the field represents a base class of a C++ structure. This attribute is always provided, and is `False` if the field is not a base class of the type that is the argument of `fields`, or if that type was not a C++ class.

`bitsize`

:   If the field is packed, or is a bitfield, then this will have a non-zero value, which is the size of the field in bits. Otherwise, this will be zero; in this case the field's size is given by its type.

`type`

:   The type of the field. This is usually an instance of `Type`, but it can be `None` in some situations.

`parent_type`

:   The type which contains this field. This is an instance of `gdb.Type`.

```

```

<!-- -->

```

)*

:   Return a new `gdb.Type` object which represents an array of this type. If one argument is given, it is the inclusive upper bound of the array; in this case the lower bound is zero. If two arguments are given, the first argument is the lower bound of the array, and the second argument is the upper bound of the array. An array's length must not be negative, but the bounds can be.

```

<!-- -->

```

)*

:   Return a new `gdb.Type` object which represents a vector of this type. If one argument is given, it is the inclusive upper bound of the vector; in this case the lower bound is zero. If two arguments are given, the first argument is the lower bound of the vector, and the second argument is the upper bound of the vector. A vector's length must not be negative, but the bounds can be.

```

The difference between an `array` and a `vector` is that arrays behave like in C: when used in expressions they decay to a pointer to the first element whereas vectors are treated as first class values.

```

```

<!-- -->

```

Function: **Type.const** *()*

:   Return a new `gdb.Type` object which represents a `const`-qualified variant of this type.

```

<!-- -->

```

Function: **Type.volatile** *()*

:   Return a new `gdb.Type` object which represents a `volatile`-qualified variant of this type.

```

<!-- -->

```

Function: **Type.unqualified** *()*

:   Return a new `gdb.Type` object which represents an unqualified variant of this type. That is, the result is neither `const` nor `volatile`.

```

<!-- -->

```

Function: **Type.range** *()*

:   Return a Python `Tuple` object that contains two elements: the low bound of the argument type and the high bound of that type. If the type does not have a range, [GDB] will raise a `gdb.error` exception (see [Exception Handling](Exception-Handling.html#Exception-Handling)).

```

<!-- -->

```

Function: **Type.reference** *()*

:   Return a new `gdb.Type` object which represents a reference to this type.

```

<!-- -->

```

Function: **Type.pointer** *()*

:   Return a new `gdb.Type` object which represents a pointer to this type.

```

<!-- -->

```

Function: **Type.strip_typedefs** *()*

:   Return a new `gdb.Type` that represents the real type, after removing all layers of typedefs.

```

<!-- -->

```

Function: **Type.target** *()*

:   Return a new `gdb.Type` object which represents the target type of this type.

```

For a pointer type, the target type is the type of the pointed-to object. For an array type (meaning C-like arrays), the target type is the type of the elements of the array. For a function or method type, the target type is the type of the return value. For a complex type, the target type is the type of the elements. For a typedef, the target type is the aliased type.

If the type does not have a target, this method will throw an exception.

```

```

<!-- -->

```

)*

:   If this `gdb.Type` is an instantiation of a template, this will return a new `gdb.Value` or `gdb.Type` which represents the value of the `n`th template argument (indexed starting at 0).

```

If this `gdb.Type` is not a template type, or if the type has fewer than `n` template arguments, this will throw an exception. Ordinarily, only C++ code will have template types.

If `block` is looked up in that scope. Otherwise, it is searched for globally.

```

```

<!-- -->

```

Function: **Type.optimized_out** *()*

:   Return `gdb.Value` instance of this type whose value is optimized out. This allows a frame decorator to indicate that the value of an argument or a local variable is not known.

Each type has a code, which indicates what category this type falls into. The available type categories are represented by constants defined in the `gdb` module:



`gdb.TYPE_CODE_PTR` 

The type is a pointer.



`gdb.TYPE_CODE_ARRAY` 

The type is an array.



`gdb.TYPE_CODE_STRUCT` 

The type is a structure.



`gdb.TYPE_CODE_UNION` 

The type is a union.



`gdb.TYPE_CODE_ENUM` 

The type is an enum.



`gdb.TYPE_CODE_FLAGS` 

A bit flags type, used for things such as status registers.



`gdb.TYPE_CODE_FUNC` 

The type is a function.



`gdb.TYPE_CODE_INT` 

The type is an integer type.



`gdb.TYPE_CODE_FLT` 

A floating point type.



`gdb.TYPE_CODE_VOID` 

The special type `void`.



`gdb.TYPE_CODE_SET` 

A Pascal set type.



`gdb.TYPE_CODE_RANGE` 

A range type, that is, an integer type with bounds.



`gdb.TYPE_CODE_STRING` 

A string type. Note that this is only used for certain languages with language-defined string types; C strings are not represented this way.



`gdb.TYPE_CODE_BITSTRING` 

A string of bits. It is deprecated.



`gdb.TYPE_CODE_ERROR` 

An unknown or erroneous type.



`gdb.TYPE_CODE_METHOD` 

A method type, as found in C++.



`gdb.TYPE_CODE_METHODPTR` 

A pointer-to-member-function.



`gdb.TYPE_CODE_MEMBERPTR` 

A pointer-to-member.



`gdb.TYPE_CODE_REF` 

A reference type.



`gdb.TYPE_CODE_RVALUE_REF` 

A C++11 rvalue reference type.



`gdb.TYPE_CODE_CHAR` 

A character type.



`gdb.TYPE_CODE_BOOL` 

A boolean type.



`gdb.TYPE_CODE_COMPLEX` 

A complex float type.



`gdb.TYPE_CODE_TYPEDEF` 

A typedef to some other type.



`gdb.TYPE_CODE_NAMESPACE` 

A C++ namespace.



`gdb.TYPE_CODE_DECFLOAT` 

A decimal floating point type.



`gdb.TYPE_CODE_INTERNAL_FUNCTION` 

A function internal to [GDB]. This is the type used to represent convenience functions.



`gdb.TYPE_CODE_XMETHOD` 

A method internal to [GDB]. This is the type used to represent xmethods (see [Writing an Xmethod](Writing-an-Xmethod.html#Writing-an-Xmethod)).



`gdb.TYPE_CODE_FIXED_POINT` 

A fixed-point number.



`gdb.TYPE_CODE_NAMESPACE` 

A Fortran namelist.

Further support for types is provided in the `gdb.types` Python module (see [gdb.types](gdb_002etypes.html#gdb_002etypes)).

---

::: header
Next: [Pretty Printing API](Pretty-Printing-API.html#Pretty-Printing-API)]
:::
```
