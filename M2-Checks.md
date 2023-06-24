---
tip: translate by openai@2023-06-23 23:57:58
...
---
description: M2 Checks (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: M2 Checks (Debugging with GDB)
lang: en
resource-type: document
title: M2 Checks (Debugging with GDB)
---
::: header
Next: [M2 Scope](M2-Scope.html#M2-Scope)]
:::

---

#### 15.4.9.7 Modula-2 Type and Range Checks

> *Warning:* in this release, [GDB] does not yet perform type or range checking.

[GDB] considers two Modula-2 variables type equivalent if:

- They are of types that have been declared equivalent via a `TYPE t1 = t2` statement

- They have been declared on the same line. (Note: This is true of the [GNU] Modula-2 compiler, but it may not be true of other compilers.)

> 他们已经在同一行声明了。（注意：这对[GNU] Modula-2编译器是正确的，但其他编译器可能不是这样。）


As long as type checking is enabled, any attempt to combine variables whose types are not equivalent is an error.

> 只要启用类型检查，任何试图合并类型不等价的变量的尝试都是一个错误。


Range checking is done on all mathematical operations, assignment, array index bounds, and all built-in functions and procedures.

> 所有数学运算、赋值、数组索引边界和所有内置函数和过程都需要进行范围检查。
