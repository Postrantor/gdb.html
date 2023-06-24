---
tip: translate by openai@2023-06-24 01:47:31
...
---
description: Range Checking (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Range Checking (Debugging with GDB)
lang: en
resource-type: document
title: Range Checking (Debugging with GDB)
---
::: header
Previous: [Type Checking](Type-Checking.html#Type-Checking)]
:::

---

#### 15.3.2 An Overview of Range Checking


In some languages (such as Modula-2), it is an error to exceed the bounds of a type; this is enforced with run-time checks. Such range checking is meant to ensure program correctness by making sure computations do not overflow, or indices on an array element access do not exceed the bounds of the array.

> 在一些语言（如Modula-2）中，超出类型范围是错误的；这是通过运行时检查来强制执行的。这种范围检查旨在通过确保计算不会溢出或数组元素访问的索引不超出数组范围来确保程序的正确性。


For expressions you use in [GDB] to treat range errors in one of three ways: ignore them, always treat them as errors and abandon the expression, or issue warnings but evaluate the expression anyway.

> 对于在GDB中使用的表达式，可以以三种方式处理范围错误：忽略它们，始终将它们视为错误并放弃表达式，或者发出警告但仍然计算表达式。


A range error can result from numerical overflow, from exceeding an array index bound, or when you type a constant that is not a member of any type. Some languages, however, do not treat overflows as an error. In many implementations of C, mathematical overflow causes the result to "wrap around" to lower values---for example, if `m` is the smallest, then

> 数值溢出、超出数组索引范围或输入的常量不是任何类型的成员都可能导致范围错误。但是，有些语言并不将溢出视为错误。在许多 C 语言的实现中，数学溢出会导致结果“折返”到较低的值，例如，如果 `m` 是最小值，那么

::: smallexample

```bash
m + 1 ⇒ s
```

:::


This, too, is specific to individual languages, and in some cases specific to individual compilers or machines. See [Supported Languages](Supported-Languages.html#Supported-Languages), for further details on specific languages.

> 这也是特定于个别语言的，有时也会特定于个别编译器或机器。有关特定语言的更多详情，请参见[支持的语言](Supported-Languages.html#Supported-Languages)。


[GDB] provides some additional commands for controlling the range checker:

> [GDB] 提供了一些额外的命令来控制范围检查器：

`set check range auto`


:   Set range checking on or off based on the current working language. See [Supported Languages](Supported-Languages.html#Supported-Languages), for the default settings for each language.

> 根据当前工作语言设置范围检查的开启或关闭。有关每种语言的默认设置，请参阅[支持的语言](Supported-Languages.html#Supported-Languages)。

`set check range on`
`set check range off`


:   Set range checking on or off, overriding the default setting for the current working language. A warning is issued if the setting does not match the language default. If a range error occurs and range checking is on, then a message is printed and evaluation of the expression is aborted.

> 设置范围检查开启或关闭，覆盖当前工作语言的默认设置。如果设置与语言默认不匹配，则会发出警告。如果发生范围错误并且范围检查打开，则会打印消息并中止表达式的求值。

`set check range warn`


:   Output messages when the [GDB] range checker detects a range error, but attempt to evaluate the expression anyway. Evaluating the expression may still be impossible for other reasons, such as accessing memory that the process does not own (a typical example from many Unix systems).

> 当[GDB]范围检查器检测到范围错误时输出消息，但仍尝试评估表达式。 由于其他原因（例如访问进程无法拥有的内存（许多Unix系统的典型示例）），评估表达式仍可能不可能。

`show check range`


:   Show the current setting of the range checker, and whether or not it is being set automatically by [GDB].

> 显示范围检查器的当前设置，以及[GDB]是否自动设置。

---

::: header
Previous: [Type Checking](Type-Checking.html#Type-Checking)]
:::
