---
tip: translate by openai@2023-06-23 14:59:37
...
---
description: Type Checking (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Type Checking (Debugging with GDB)
lang: en
resource-type: document
title: Type Checking (Debugging with GDB)
-----------------------------------------

::: header
Next: [Range Checking](Range-Checking.html#Range-Checking)]
:::

---

#### 15.3.1 An Overview of Type Checking

Some languages, such as C and C++, are strongly typed, meaning that the arguments to operators and functions have to be of the correct type, otherwise an error occurs. These checks prevent type mismatch errors from ever causing any run-time problems. For example,

> 一些语言，如 C 和 C++，是强类型的，这意味着操作符和函数的参数必须是正确的类型，否则会发生错误。这些检查可以防止类型不匹配的错误在运行时出现问题。例如，

::: smallexample

```bash
int klass::my_method(char *b) 

(gdb) print obj.my_method (0)
$1 = 2
```

```bash
but
```

```bash
(gdb) print obj.my_method (0x1234)
Cannot resolve method klass::my_method to any overloaded instance
```

:::

The second example fails because in C++ the integer constant '`0x1234`' is not type-compatible with the pointer parameter type.

> 第二个示例失败，因为在 C++ 中，整数常量'0x1234'与指针参数类型不兼容。

For the expressions you use in [GDB] successfully evaluates expressions like the second example above.

> 对于在 GDB 中使用的表达式，可以成功地评估像第二个示例一样的表达式。

Even if type checking is off, there may be other reasons related to type that prevent [GDB] does not know how to add an `int` and a `struct foo`. These particular type errors have nothing to do with the language in use and usually arise from expressions which make little sense to evaluate anyway.

> 即使类型检查关闭了，也可能有其他与类型有关的原因阻止 GDB 不知道如何将一个 int 和一个 struct foo 相加。这些特定的类型错误与所使用的语言无关，通常是由没有意义的表达式引起的。

[GDB] provides some additional commands for controlling type checking:

> [GDB] 提供了一些额外的命令来控制类型检查：

`set check type on`
`set check type off`

:   Set strict type checking on or off. If any type mismatches occur in evaluating an expression while type checking is on, [GDB] prints a message and aborts evaluation of the expression.

> 开启或关闭严格类型检查。如果在开启类型检查的情况下，在求值表达式时发生类型不匹配，[GDB]就会打印一条消息并中止表达式的求值。

`show check type`

:   Show the current setting of type checking and whether [GDB] is enforcing strict type checking rules.

> 查看当前类型检查设置以及[GDB]是否正在强制执行严格的类型检查规则。

---

::: header
Next: [Range Checking](Range-Checking.html#Range-Checking)]
:::
