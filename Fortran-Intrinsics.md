---
tip: translate by openai@2023-06-23 21:16:39
...
---
description: Fortran Intrinsics (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Fortran Intrinsics (Debugging with GDB)
lang: en
resource-type: document
title: Fortran Intrinsics (Debugging with GDB)
---
::: header
Next: [Special Fortran Commands](Special-Fortran-Commands.html#Special-Fortran-Commands)]
:::

---

#### 15.4.6.3 Fortran Intrinsics


Fortran provides a large set of intrinsic procedures. [GDB] implements an incomplete subset of those procedures and their overloads. Some of these procedures take an optional `KIND` parameter, see [Fortran Types](Fortran-Types.html#Fortran-Types).

> Fortran提供了一系列内置程序。[GDB]实现了这些程序及其重载的不完整子集。其中一些程序接受可选的`KIND`参数，详见[Fortran Types](Fortran-Types.html#Fortran-Types)。

`ABS(a)`


:   Computes the absolute value of its argument `a`. Currently not supported for `Complex` arguments.

> 计算其参数`a`的绝对值。目前不支持复数参数。

`ALLOCATE(array)`

:   Returns whether `array` is allocated or not.

`ASSOCIATED(pointer [, target])`

:   Returns the association status of the pointer `pointer`.

`CEILING(a [, kind])`


:   Computes the least integer greater than or equal to `a` specifies the kind of the return type `Integer(kind)`.

> 计算大于或等于a的最小整数，指定返回类型为Integer(kind)。

`CMPLX(x [, y [, kind]])`


:   Returns a complex number where `x` specifies the kind of the return type `Complex(kind)`.

> 返回一个复数，其中x指定返回类型Complex(kind)。

`FLOOR(a [, kind])`


:   Computes the greatest integer less than or equal to `a` specifies the kind of the return type `Integer(kind)`.

> 计算小于或等于`a`的最大整数，指定返回类型为`Integer（kind）`。

`KIND(a)`


:   Returns the kind value of the argument `a`, see [Fortran Types](Fortran-Types.html#Fortran-Types).

> 返回参数`a`的类型值，请参阅[Fortran Types](Fortran-Types.html#Fortran-Types)。

`LBOUND(array [, dim [, kind]])`


:   Returns the lower bounds of an `array` specifies the kind of the return type `Integer(kind)`.

> 返回一个数组的下界，指定返回类型为整数（kind）。

`LOC(x)`

:   Returns the address of `x` as an `Integer`.

`MOD(a, p)`

:   Computes the remainder of the division of `a`.

`MODULO(a, p)`

:   Computes the `a`.

`RANK(a)`

:   Returns the rank of a scalar or array (scalars have rank `0`).

`SHAPE(a)`

:   Returns the shape of a scalar or array (scalars have shape '`()`').

`SIZE(array[, dim [, kind]])`


:   Returns the extent of `array` specifies the kind of the return type `Integer(kind)`.

> 返回数组的范围，指定返回类型的种类为整数（kind）。

`UBOUND(array [, dim [, kind]])`


:   Returns the upper bounds of an `array` specifies the kind of the return type `Integer(kind)`.

> 返回一个数组的上限，指定返回类型为整数（kind）。

---

::: header
Next: [Special Fortran Commands](Special-Fortran-Commands.html#Special-Fortran-Commands)]
:::
