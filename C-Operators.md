---
tip: translate by openai@2023-06-23 18:42:52
...
---
description: C Operators (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: C Operators (Debugging with GDB)
lang: en
resource-type: document
title: C Operators (Debugging with GDB)
---
::: header
Next: [C Constants](C-Constants.html#C-Constants)]
:::

---

#### 15.4.1.1 C and C++ Operators


Operators must be defined on values of specific types. For instance, `+` is defined on numbers, but not on structures. Operators are often defined on groups of types.

> 运算符必须定义在特定类型的值上。例如，`+`定义在数字上，但不在结构上。运算符通常定义在类型组上。


For the purposes of C and C++, the following definitions hold:

> 对于C和C++的目的，以下定义是有效的：


- *Integral types* include `int` with any of its storage-class specifiers; `char`; `enum`; and, for C++, `bool`.

> 整数类型包括带有任何存储类说明符的`int`; `char`; `enum`; 对于C++，还有 `bool`。

- *Floating-point types* include `float`, `double`, and `long double` (if supported by the target platform).

> 浮点类型包括`float`、`double`和`long double`（如果目标平台支持）。
- *Pointer types* include all types defined as `(type *)`.
- *Scalar types* include all of the above.


The following operators are supported. They are listed here in order of increasing precedence:

> 以下操作符受支持。它们按照优先级递增的顺序列出：

`,`


:   The comma or sequencing operator. Expressions in a comma-separated list are evaluated from left to right, with the result of the entire expression being the last expression evaluated.

> 逗号或序列操作符。在逗号分隔的列表中的表达式从左到右求值，整个表达式的结果是最后一个被求值的表达式。

`=`


:   Assignment. The value of an assignment expression is the value assigned. Defined on scalar types.

> 赋值表达式的值是被赋予的值。定义在标量类型上。

`op=`


:   Used in an expression of the form `a op= b`, and translated to `a = a op b`. `op=` and `=` have the same precedence. The operator `op` is any one of the operators `|`, `^`, `&`, `<<`, `>>`, `+`, `-`, `*`, `/`, `%`.

> 在形式为`a op= b`的表达式中使用，并翻译为`a = a op b`。 `op=`和`=`具有相同的优先级。 操作符`op`是`|`、`^`、`&`、`<<`、`>>`、`+`、`-`、`*`、`/`和`%`中的任何一个。

`?:`


:   The ternary operator. `a ? b : c` can be thought of as: if `a` should be of an integral type.

> 三元运算符“a ? b : c”可以被看作：如果a应该是整型的。

`||`


:   Logical [OR]. Defined on integral types.

> 逻辑[或]。针对整数类型定义。

`&&`


:   Logical [AND]. Defined on integral types.

> 逻辑[AND]。定义在整数类型上。

`|`


:   Bitwise [OR]. Defined on integral types.

> 位元運算[OR]。定義於整數類型。

`^`


:   Bitwise exclusive-[OR]. Defined on integral types.

> 位元排他或（Bitwise exclusive-OR），定義於整數類型。

`&`


:   Bitwise [AND]. Defined on integral types.

> 位元運算[AND]。對整數型別定義。

`==, !=`


:   Equality and inequality. Defined on scalar types. The value of these expressions is 0 for false and non-zero for true.

> 平等与不平等。在标量类型上定义。这些表达式的值为假为0，为真为非零。

`<, >, <=, >=`


:   Less than, greater than, less than or equal, greater than or equal. Defined on scalar types. The value of these expressions is 0 for false and non-zero for true.

> 小于，大于，小于等于，大于等于。 在标量类型上定义。 这些表达式的值为false时为0，为true时为非零。

`<<, >>`


:   left shift, and right shift. Defined on integral types.

> 左移和右移，针对整数类型定义。

`@`


:   The [GDB] "artificial array" operator (see [Expressions](Expressions.html#Expressions)).

> GDB的"人工数组"操作符（参见[表达式](Expressions.html#Expressions)）。

`+, -`


:   Addition and subtraction. Defined on integral types, floating-point types and pointer types.

> 加法和减法。定义在整数类型、浮点类型和指针类型上。

`*, /, %`


:   Multiplication, division, and modulus. Multiplication and division are defined on integral and floating-point types. Modulus is defined on integral types.

> 乘法、除法和取模。乘法和除法可以用整数和浮点数来定义。取模只能用整数来定义。

`++, --`


:   Increment and decrement. When appearing before a variable, the operation is performed before the variable is used in an expression; when appearing after it, the variable's value is used before the operation takes place.

> 当出现在变量之前时，操作会在变量被用于表达式之前执行；当出现在变量之后时，变量的值会在操作发生之前使用。

`*`


:   Pointer dereferencing. Defined on pointer types. Same precedence as `++`.

> 指针取值。定义在指针类型上。与“++”具有相同的优先级。

`&`


:   Address operator. Defined on variables. Same precedence as `++`.

> 地址运算符。定义在变量上。与“++”具有相同的优先级。

```
For debugging C++, [GDB]') is stored.
```

`-`


:   Negative. Defined on integral and floating-point types. Same precedence as `++`.

> 否定。定义在整数和浮点类型上。与“++”具有相同的优先级。

`!`


:   Logical negation. Defined on integral types. Same precedence as `++`.

> 逻辑否定。在整数类型上定义。与“++”具有相同的优先级。

`~`


:   Bitwise complement operator. Defined on integral types. Same precedence as `++`.

> 位元補數運算子。定義於整數類型。優先級與'++'相同。

`., ->`


:   Structure member, and pointer-to-structure member. For convenience, [GDB] regards the two as equivalent, choosing whether to dereference a pointer based on the stored type information. Defined on `struct` and `union` data.

> 结构成员和指向结构成员的指针。为了方便起见，[GDB]将两者视为等价，根据存储的类型信息来决定是否解引用指针。定义在`struct`和`union`数据上。

`.*, ->*`


:   Dereferences of pointers to members.

> 指向成员的指针解引用。

``


:   Array indexing. `a[i]` is defined as `*(a+i)`. Same precedence as `->`.

> 数组索引。`a[i]`定义为`*(a+i)`，优先级与`->`相同。

`()`


:   Function parameter list. Same precedence as `->`.

> 参数列表函数。 与“->”具有相同的优先级。

`::`


:   C++ scope resolution operator. Defined on `struct`, `union`, and `class` types.

> C++ 范围解析运算符。定义在结构体、联合体和类型上。

`::`


:   Doubled colons also represent the [GDB] scope operator (see [Expressions](Expressions.html#Expressions)). Same precedence as `::`, above.

> 双冒号也表示GDB作用域运算符（参见表达式），优先级与上面的`::`相同。


If an operator is redefined in the user code, [GDB] usually attempts to invoke the redefined version instead of using the operator's predefined meaning.

> 如果用户代码中重新定义了操作符，[GDB]通常会尝试调用重新定义的版本，而不是使用操作符的预定义含义。

---

::: header
Next: [C Constants](C-Constants.html#C-Constants)]
:::
