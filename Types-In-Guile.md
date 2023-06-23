---
tip: translate by openai@2023-06-23 15:01:54
...
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

> [GDB] 用<gdb:type>类型的对象表示来自下层的类型。


The following type-related procedures are provided by the `(gdb)` module.

> `(gdb)` 模块提供了以下与类型相关的程序。


Scheme Procedure: **type?** *object*

> 方案程序：**type？** *object*


:   Return `#t` if `object` is an object of type `<gdb:type>`. Otherwise return `#f`.

> 如果对象是<gdb:type>类型的对象，则返回#t，否则返回#f。

```

```

*


:   This function looks up a type by its `name`, which must be a string.

> 这个函数通过其名称（必须是字符串）查找类型。

```
If `block` is looked up in that scope. Otherwise, it is searched for globally.

Ordinarily, this function will return an instance of `<gdb:type>`. If the named type cannot be found, it will throw an exception.
```

```

```


Scheme Procedure: **type-code** *type*

> 方案程序：**type-code** *type*


:   Return the type code of `type`. The type code will be one of the `TYPE_CODE_` constants defined below.

> 返回`type`的类型代码。类型代码将是下面定义的`TYPE_CODE_`常量之一。

```

```


Scheme Procedure: **type-tag** *type*

> 方案程序：**类型标记** *类型*


:   Return the tag name of `type`. The tag name is the name after `struct`, `union`, or `enum` in C and C++; not all languages have this concept. If this type has no tag name, then `#f` is returned.

> 返回类型`type`的标签名称。标签名称是C和C++中`struct`、`union`或`enum`之后的名称；不是所有的语言都有这个概念。如果这个类型没有标签名称，则返回`#f`。

```

```


Scheme Procedure: **type-name** *type*

> 方案程序：**类型名称** *类型*


:   Return the name of `type`. If this type has no name, then `#f` is returned.

> 返回类型的名称。如果这个类型没有名称，则返回#f。

```

```


Scheme Procedure: **type-print-name** *type*

> 方案程序：** type-print-name ** * type *


:   Return the print name of `type`"` is returned.

> 返回`type`的打印名称

```

```


Scheme Procedure: **type-sizeof** *type*

> 方案流程：**type-sizeof** *type*


:   Return the size of this type, in target `char` units. Usually, a target's `char` type will be an 8-bit byte. However, on some unusual platforms, this type may have a different size.

> 返回这种类型的大小，以目标`char`单位表示。通常，目标的`char`类型将是一个8位字节。但是，在一些不寻常的平台上，这种类型可能具有不同的大小。

```

```


Scheme Procedure: **type-strip-typedefs** *type*

> 方案程序：**type-strip-typedefs** *type*


:   Return a new `<gdb:type>` that represents the real type of `type`, after removing all layers of typedefs.

> 返回一个新的<gdb:type>，它代表着在删除所有的typedef层之后的type的真实类型。

```

```

*


:   Return a new `<gdb:type>` object which represents an array of this type. If one argument is given, it is the inclusive upper bound of the array; in this case the lower bound is zero. If two arguments are given, the first argument is the lower bound of the array, and the second argument is the upper bound of the array. An array's length must not be negative, but the bounds can be.

> 返回一个新的`<gdb:type>`对象，它表示这种类型的数组。如果给出一个参数，它是数组的包容上界；在这种情况下，下界为零。如果给出两个参数，第一个参数是数组的下界，第二个参数是数组的上界。数组的长度不能为负，但边界可以。

```

```

*


:   Return a new `<gdb:type>` object which represents a vector of this type. If one argument is given, it is the inclusive upper bound of the vector; in this case the lower bound is zero. If two arguments are given, the first argument is the lower bound of the vector, and the second argument is the upper bound of the vector. A vector's length must not be negative, but the bounds can be.

> 返回一个新的<gdb:type>对象，它表示该类型的向量。如果给出一个参数，则该参数是向量的包含上界；在这种情况下，下界为零。如果给出两个参数，则第一个参数是向量的下界，第二个参数是向量的上界。向量的长度不能为负，但边界可以。

```
The difference between an `array` and a `vector` is that arrays behave like in C: when used in expressions they decay to a pointer to the first element whereas vectors are treated as first class values.
```

```

```


Scheme Procedure: **type-pointer** *type*

> 方案程序：**type-pointer** *type*


:   Return a new `<gdb:type>` object which represents a pointer to `type`.

> 返回一个新的<gdb:type>对象，它表示一个指向类型的指针。

```

```


Scheme Procedure: **type-range** *type*

> 方案程序：**type-range** *type*


:   Return a list of two elements: the low bound and high bound of `type` does not have a range, an exception is thrown.

> 返回一个两个元素的列表：`type`的下限和上限，如果没有范围，则抛出异常。

```

```


Scheme Procedure: **type-reference** *type*

> 方案程序：**类型引用** *类型*


:   Return a new `<gdb:type>` object which represents a reference to `type`.

> 返回一个新的`<gdb:type>`对象，它表示对`type`的引用。

```

```


Scheme Procedure: **type-target** *type*

> 方案程序：**type-target** *type*


:   Return a new `<gdb:type>` object which represents the target type of `type`.

> 返回一个新的`<gdb:type>`对象，它代表了`type`的目标类型。

```
For a pointer type, the target type is the type of the pointed-to object. For an array type (meaning C-like arrays), the target type is the type of the elements of the array. For a function or method type, the target type is the type of the return value. For a complex type, the target type is the type of the elements. For a typedef, the target type is the aliased type.

If the type does not have a target, this method will throw an exception.
```

```

```


Scheme Procedure: **type-const** *type*

> 方案程序：**type-const** *type*


:   Return a new `<gdb:type>` object which represents a `const`-qualified variant of `type`.

> 返回一个新的<gdb:type>对象，它表示类型的const限定变体。

```

```


Scheme Procedure: **type-volatile** *type*

> 方案程序：**type-volatile** *type*


:   Return a new `<gdb:type>` object which represents a `volatile`-qualified variant of `type`.

> 返回一个新的<gdb:type>对象，它表示类型的volatile限定变体。

```

```


Scheme Procedure: **type-unqualified** *type*

> 方案程序：**type-unqualified** *type*


:   Return a new `<gdb:type>` object which represents an unqualified variant of `type`. That is, the result is neither `const` nor `volatile`.

> 返回一个新的`<gdb:type>`对象，它表示一个未经限定的类型变体。也就是说，结果既不是`const`也不是`volatile`。

```

```


Scheme Procedure: **type-num-fields**

> 方案程序：**type-num-fields**


:   Return the number of fields of `<gdb:type>` `type`.

> 返回<gdb:type>类型的字段数量。

```

```


Scheme Procedure: **type-fields** *type*

> 方案程序：**type-fields** *type*


:   Return the fields of `type` as a list. For structure and union types, `fields` has the usual meaning. Range types have two fields, the minimum and maximum values. Enum types have one field per enum constant. Function and method types have one field per parameter. The base types of C++ classes are also represented as fields. If the type has no fields, or does not fit into one of these categories, an empty list will be returned. See [Fields of a type in Guile](#Fields-of-a-type-in-Guile).

> 返回类型的字段作为一个列表。对于结构体和联合类型，`fields`具有通常的含义。范围类型有两个字段，最小值和最大值。枚举类型有一个字段每个枚举常量。函数和方法类型有一个字段每个参数。C++类的基本类型也被表示为字段。如果类型没有字段，或者不属于这些类别之一，将返回一个空列表。请参阅[Guile中的类型字段](#Fields-of-a-type-in-Guile)。

```

```


Scheme Procedure: **make-field-iterator** *type*

> 方案程序：**make-field-iterator** *type*


:   Return the fields of `type` as a \<gdb:iterator\> object. See [Iterators In Guile](Iterators-In-Guile.html#Iterators-In-Guile).

> 返回`type`字段作为一个<gdb:iterator>对象。参见[Guile中的迭代器](Iterators-In-Guile.html#Iterators-In-Guile)。

```

```


Scheme Procedure: **type-field** *type field-name*

> 方案程序：**类型字段** *类型字段名*


:   Return field named `field-name`, an exception is thrown.

> 如果没有找到名为“field-name”的字段，则抛出异常。

```
For example, if `some-type` is a `<gdb:type>` instance holding a structure type, you can access its `foo` field with:

::: smallexample
``` smallexample

(define bar (type-field some-type "foo"))

> (定义bar（类型字段some-type “foo”）)
```

:::

`bar` will be a `<gdb:field>` object.

```

```

```


Scheme Procedure: **type-has-field?** *type name*

> 方案程序：**type-has-field？** *类型名称*


:   Return `#t` if `<gdb:type>` `type`. Otherwise return `#f`.

> 如果<gdb:type>类型为'type'，则返回#t。否则返回#f。


Each type has a code, which indicates what category this type falls into. The available type categories are represented by constants defined in the `(gdb)` module:

> 每种类型都有一个代码，用来表示该类型属于哪个类别。可用的类型类别由`(gdb)`模块中定义的常量表示。

`TYPE_CODE_PTR` 


:   The type is a pointer.

> 这是一个指针。

`TYPE_CODE_ARRAY` 


:   The type is an array.

> 这是一个数组。

`TYPE_CODE_STRUCT` 


:   The type is a structure.

> 类型是一种结构。

`TYPE_CODE_UNION` 


:   The type is a union.

> 这种类型是联合类型。

`TYPE_CODE_ENUM` 


:   The type is an enum.

> 这是一个枚举类型。

`TYPE_CODE_FLAGS` 


:   A bit flags type, used for things such as status registers.

> 一种位标志类型，用于状态寄存器等事物。

`TYPE_CODE_FUNC` 


:   The type is a function.

> 这种类型是一个函数。

`TYPE_CODE_INT` 


:   The type is an integer type.

> 这是一种整数类型。

`TYPE_CODE_FLT` 


:   A floating point type.

> 浮点类型。

`TYPE_CODE_VOID` 


:   The special type `void`.

> 特殊类型“void”。

`TYPE_CODE_SET` 

:   A Pascal set type.

`TYPE_CODE_RANGE` 


:   A range type, that is, an integer type with bounds.

> 一种范围类型，也就是一种带有界限的整数类型。

`TYPE_CODE_STRING` 


:   A string type. Note that this is only used for certain languages with language-defined string types; C strings are not represented this way.

> 字符串类型。请注意，这仅用于某些具有语言定义字符串类型的语言；C字符串不是用这种方式表示的。

`TYPE_CODE_BITSTRING` 


:   A string of bits. It is deprecated.

> 一串位元組。它已經被廢除了。

`TYPE_CODE_ERROR` 


:   An unknown or erroneous type.

> 未知或错误的类型。

`TYPE_CODE_METHOD` 


:   A method type, as found in C++.

> 一种在C++中发现的方法类型。

`TYPE_CODE_METHODPTR` 


:   A pointer-to-member-function.

> 指向成员函数的指针

`TYPE_CODE_MEMBERPTR` 


:   A pointer-to-member.

> 指向成员的指针。

`TYPE_CODE_REF` 

:   A reference type.

`TYPE_CODE_RVALUE_REF` 


:   A C++11 rvalue reference type.

> C++11的右值引用类型。

`TYPE_CODE_CHAR` 

:   A character type.

`TYPE_CODE_BOOL` 

:   A boolean type.

`TYPE_CODE_COMPLEX` 


:   A complex float type.

> 复杂的浮点类型。

`TYPE_CODE_TYPEDEF` 


:   A typedef to some other type.

> 定义类型别名到其他类型。

`TYPE_CODE_NAMESPACE` 

:   A C++ namespace.

`TYPE_CODE_DECFLOAT` 


:   A decimal floating point type.

> 十进制浮点类型。

`TYPE_CODE_INTERNAL_FUNCTION` 


:   A function internal to [GDB]. This is the type used to represent convenience functions (see [Convenience Funs](Convenience-Funs.html#Convenience-Funs)).

> 一个内部函数[GDB]。这是一种用来表示便利函数的类型（参见[便利函数](Convenience-Funs.html#Convenience-Funs)）。

```

```

`gdb.TYPE_CODE_XMETHOD` 


:   A method internal to [GDB]. This is the type used to represent xmethods (see [Writing an Xmethod](Writing-an-Xmethod.html#Writing-an-Xmethod)).

> 这是GDB内部使用的一种方法。这种类型用于表示xmethods（参见[编写Xmethod](Writing-an-Xmethod.html#Writing-an-Xmethod)）。

```

```

`gdb.TYPE_CODE_FIXED_POINT` 


:   A fixed-point number.

> 固定点数。

```

```

`gdb.TYPE_CODE_NAMESPACE` 

:   A Fortran namelist.


Further support for types is provided in the `(gdb types)` Guile module (see [Guile Types Module](Guile-Types-Module.html#Guile-Types-Module)).

> 更多关于类型的支持可以在`(gdb types)` Guile模块中找到（参见[Guile Types Module](Guile-Types-Module.html#Guile-Types-Module)）。




Each field is represented as an object of type `<gdb:field>`.

> 每个字段都表示为<gdb:field>类型的对象。


The following field-related procedures are provided by the `(gdb)` module:

> 以下与字段相关的程序由(gdb)模块提供：


Scheme Procedure: **field?** *object*

> 方案程序：**field？** *object*


:   Return `#t` if `object` is an object of type `<gdb:field>`. Otherwise return `#f`.

> 如果对象是<gdb:field>类型的对象，则返回#t。否则返回#f。

```

```


Scheme Procedure: **field-name** *field*

> 方案程序：**字段名** *字段*


:   Return the name of the field, or `#f` for anonymous fields.

> 返回字段的名称，或者使用“#f”表示匿名字段。

```

```


Scheme Procedure: **field-type** *field*

> 方案程序：**field-type** *field*


:   Return the type of the field. This is usually an instance of `<gdb:type>`, but it can be `#f` in some situations.

> 返回字段的类型。通常是一个<gdb:type>的实例，但在某些情况下可能是#f。

```

```


Scheme Procedure: **field-enumval** *field*

> 方案程序：**field-enumval** *field*


:   Return the enum value represented by `<gdb:field>` `field`.

> 返回由`<gdb:field>` `field`表示的枚举值。

```

```


Scheme Procedure: **field-bitpos** *field*

> 方案程序：**field-bitpos** *field*


:   Return the bit position of `<gdb:field>` `field`. This attribute is not available for `static` fields (as in C++).

> 返回`<gdb:field>` `field`的位置。此属性不适用于C++中的`static`字段。

```

```


Scheme Procedure: **field-bitsize** *field*

> 方案程序：**field-bitsize** *field*


:   If the field is packed, or is a bitfield, return the size of `<gdb:field>` `field` in bits. Otherwise, zero is returned; in which case the field's size is given by its type.

> 如果该字段是填充字段或位域，则返回<gdb:field>字段`field`的位数。否则，返回零；在这种情况下，字段的大小由其类型给出。

```

```


Scheme Procedure: **field-artificial?** *field*

> 方案程序：** field-artificial？** * field *


:   Return `#t` if the field is artificial, usually meaning that it was provided by the compiler and not the user. Otherwise return `#f`.

> 如果该字段是人工制作的，通常意味着它是由编译器提供的而不是用户提供的，则返回#t，否则返回#f。

```

```


Scheme Procedure: **field-base-class?** *field*

> 方案程序：**field-base-class？** *field*


:   Return `#t` if the field represents a base class of a C++ structure. Otherwise return `#f`.

> 如果该字段表示C++结构的基类，则返回#t，否则返回#f。

---

::: header
Next: [Guile Pretty Printing API](Guile-Pretty-Printing-API.html#Guile-Pretty-Printing-API)]
:::
```
