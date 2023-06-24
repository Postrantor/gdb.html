---
tip: translate by openai@2023-06-23 18:32:32
...
---
description: Built-In Func/Proc (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Built-In Func/Proc (Debugging with GDB)
lang: en
resource-type: document
title: Built-In Func/Proc (Debugging with GDB)
---
::: header
Next: [M2 Constants](M2-Constants.html#M2-Constants)]
:::

---

#### 15.4.9.2 Built-in Functions and Procedures


Modula-2 also makes available several built-in procedures and functions. In describing these, the following metavariables are used:

> Modula-2还提供了几种内置的程序和函数。在描述这些函数时，使用以下元变量：

`a`


:   represents an `ARRAY` variable.

> `:`代表一个`数组`变量。

`c`


:   represents a `CHAR` constant or variable.

> ':代表一个`CHAR`常量或变量。

`i`


:   represents a variable or constant of integral type.

> 表示一个整型变量或常量。

`m`


:   represents an identifier that belongs to a set. Generally used in the same function with the metavariable `s`).

> `:`代表属于一个集合的标识符。通常与元变量`s`一起使用。

`n`


:   represents a variable or constant of integral or floating-point type.

> ': 代表一个整数或浮点类型的变量或常量。

`r`


:   represents a variable or constant of floating-point type.

> 表示浮点类型的变量或常量。

`t`

:   represents a type.

`v`


:   represents a variable.

> :代表一个变量。

`x`


:   represents a variable or constant of one of many types. See the explanation of the function for details.

> ": 代表了多种类型的变量或常量。详情请参阅函数的解释。


All Modula-2 built-in procedures also return a result, described below.

> 所有的Modula-2内置过程也会返回一个结果，如下所述。

`ABS(n)`


:   Returns the absolute value of `n`.

> 返回n的绝对值。

`CAP(c)`


:   If `c` is a lower case letter, it returns its upper case equivalent, otherwise it returns its argument.

> 如果`c`是一个小写字母，它会返回它的大写形式，否则它会返回它的参数。

`CHR(i)`


:   Returns the character whose ordinal value is `i`.

> 返回其序数值为i的字符。

`DEC(v)`


:   Decrements the value in the variable `v` by one. Returns the new value.

> 减少变量`v`的值1。返回新值。

`DEC(v,i)`


:   Decrements the value in the variable `v`. Returns the new value.

> 减少变量`v`中的值。返回新值。

`EXCL(m,s)`


:   Removes the element `m`. Returns the new set.

> 移除元素'm'，返回新集合。

`FLOAT(i)`


:   Returns the floating point equivalent of the integer `i`.

> 返回整数i的浮点数等价物。

`HIGH(a)`


:   Returns the index of the last member of `a`.

> 返回a的最后一个成员的索引。

`INC(v)`


:   Increments the value in the variable `v` by one. Returns the new value.

> 增加变量`v`中的值1。返回新值。

`INC(v,i)`


:   Increments the value in the variable `v`. Returns the new value.

> 增加变量`v`中的值。返回新值。

`INCL(m,s)`


:   Adds the element `m` if it is not already there. Returns the new set.

> 如果不存在元素'm，则添加它。返回新的集合。

`MAX(t)`


:   Returns the maximum value of the type `t`.

> 返回类型't'的最大值。

`MIN(t)`


:   Returns the minimum value of the type `t`.

> 返回类型't'的最小值。

`ODD(i)`


:   Returns boolean TRUE if `i` is an odd number.

> 返回布尔值TRUE，如果`i`是一个奇数。

`ORD(x)`


:   Returns the ordinal value of its argument. For example, the ordinal value of a character is its [ASCII] must be of an ordered type, which include integral, character and enumerated types.

> 返回其参数的序数值。例如，字符的序数值是它的[ASCII]必须是一种有序类型，其中包括整数、字符和枚举类型。

`SIZE(x)`


:   Returns the size of its argument. The argument `x` can be a variable or a type.

> 返回其参数的大小。参数`x`可以是一个变量或类型。

`TRUNC(r)`


:   Returns the integral part of `r`.

> 返回r的整数部分。

`TSIZE(x)`


:   Returns the size of its argument. The argument `x` can be a variable or a type.

> 返回其参数的大小。参数`x`可以是变量或类型。

`VAL(t,i)`


:   Returns the member of the type `t`.

> 返回类型`t`的成员。

> *Warning:* Sets and their operations are not yet supported, so [GDB] treats the use of procedures `INCL` and `EXCL` as an error.

---

::: header
Next: [M2 Constants](M2-Constants.html#M2-Constants)]
:::
