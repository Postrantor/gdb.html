---
tip: translate by openai@2023-06-24 10:25:19
...
---
description: M2 Operators (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: M2 Operators (Debugging with GDB)
lang: en
resource-type: document
title: M2 Operators (Debugging with GDB)
---
::: header
Next: [Built-In Func/Proc](Built_002dIn-Func_002fProc.html#Built_002dIn-Func_002fProc)]
:::

---

#### 15.4.9.1 Operators


Operators must be defined on values of specific types. For instance, `+` is defined on numbers, but not on structures. Operators are often defined on groups of types. For the purposes of Modula-2, the following definitions hold:

> 运算符必须在特定类型的值上定义。例如，“+”是定义在数字上的，而不是在结构上的。运算符通常定义在一组类型上。就Modula-2而言，以下定义适用：

- *Integral types* consist of `INTEGER`, `CARDINAL`, and their subranges.
- *Character types* consist of `CHAR` and its subranges.
- *Floating-point types* consist of `REAL`.
- *Pointer types* consist of anything declared as `POINTER TO type`.
- *Scalar types* consist of all of the above.
- *Set types* consist of `SET` and `BITSET` types.
- *Boolean types* consist of `BOOLEAN`.


The following operators are supported, and appear in order of increasing precedence:

> 以下运算符受支持，按照优先级递增排列：

`,`

:   Function argument or array index separator.

`:=`

:   Assignment. The value of `var`.

`<, >`


:   Less than, greater than on integral, floating-point, or enumerated types.

> 小于、大于整数、浮点数或枚举类型。

`<=, >=`


:   Less than or equal to, greater than or equal to on integral, floating-point and enumerated types, or set inclusion on set types. Same precedence as `<`.

> 小于或等于、大于或等于整数、浮点数和枚举类型，或者集合类型的集合包含。与“<”具有相同的优先级。

`=, <>, #`


:   Equality and two ways of expressing inequality, valid on scalar types. Same precedence as `<`. In [GDB] scripts, only `<>` is available for inequality, since `#` conflicts with the script comment character.

> 平等和表示不等式的两种方法，在标量类型上有效。与`<`具有相同的优先级。在[GDB]脚本中，只有`<>`可用于不等式，因为`#`与脚本注释字符冲突。

`IN`


:   Set membership. Defined on set types and the types of their members. Same precedence as `<`.

> 集合成员关系。定义在集合类型及其成员类型上。与“<”具有相同的优先级。

`OR`

:   Boolean disjunction. Defined on boolean types.

`AND, &`

:   Boolean conjunction. Defined on boolean types.

`@`


:   The [GDB] "artificial array" operator (see [Expressions](Expressions.html#Expressions)).

> GDB中的“人工数组”操作符（参见[表达式](Expressions.html#Expressions)）。

`+, -`


:   Addition and subtraction on integral and floating-point types, or union and difference on set types.

> 加法和减法在整数和浮点类型上，或集合类型上的并集和差集。

`*`


:   Multiplication on integral and floating-point types, or set intersection on set types.

> 乘法运算在整数和浮点类型上，或集合类型上的集合交集。

`/`


:   Division on floating-point types, or symmetric set difference on set types. Same precedence as `*`.

> 浮点型的除法或集合类型的对称集合差异。与“*”具有相同的优先级。

`DIV, MOD`


:   Integer division and remainder. Defined on integral types. Same precedence as `*`.

> 整数除法和余数。定义在整数类型上。与“*”具有相同的优先级。

`-`

:   Negative. Defined on `INTEGER` and `REAL` data.

`^`

:   Pointer dereferencing. Defined on pointer types.

`NOT`

:   Boolean negation. Defined on boolean types. Same precedence as `^`.

`.`


:   `RECORD` field selector. Defined on `RECORD` data. Same precedence as `^`.

> 记录字段选择器。定义在记录数据上。与^具有相同的优先级。

``

:   Array indexing. Defined on `ARRAY` data. Same precedence as `^`.

`()`


:   Procedure argument list. Defined on `PROCEDURE` objects. Same precedence as `^`.

> 参数列表程序。定义在“程序”对象上。与“^”具有相同的优先级。

`::, .`

:   [GDB] and Modula-2 scope operators.

> *Warning:* Set expressions and their operations are not yet supported, so [GDB] treats the use of the operator `IN`, or the use of operators `+`, `-`, `*`, `/`, `=`, , `<>`, `#`, `<=`, and `>=` on sets as an error.

---

::: header
Next: [Built-In Func/Proc](Built_002dIn-Func_002fProc.html#Built_002dIn-Func_002fProc)]
:::
