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

For expressions you use in [GDB] to treat range errors in one of three ways: ignore them, always treat them as errors and abandon the expression, or issue warnings but evaluate the expression anyway.

A range error can result from numerical overflow, from exceeding an array index bound, or when you type a constant that is not a member of any type. Some languages, however, do not treat overflows as an error. In many implementations of C, mathematical overflow causes the result to "wrap around" to lower values---for example, if `m` is the smallest, then

::: smallexample

```bash
m + 1 ⇒ s
```

:::

This, too, is specific to individual languages, and in some cases specific to individual compilers or machines. See [Supported Languages](Supported-Languages.html#Supported-Languages), for further details on specific languages.

[GDB] provides some additional commands for controlling the range checker:

`set check range auto`

:   Set range checking on or off based on the current working language. See [Supported Languages](Supported-Languages.html#Supported-Languages), for the default settings for each language.

`set check range on`
`set check range off`

:   Set range checking on or off, overriding the default setting for the current working language. A warning is issued if the setting does not match the language default. If a range error occurs and range checking is on, then a message is printed and evaluation of the expression is aborted.

`set check range warn`

:   Output messages when the [GDB] range checker detects a range error, but attempt to evaluate the expression anyway. Evaluating the expression may still be impossible for other reasons, such as accessing memory that the process does not own (a typical example from many Unix systems).

`show check range`

:   Show the current setting of the range checker, and whether or not it is being set automatically by [GDB].

---

::: header
Previous: [Type Checking](Type-Checking.html#Type-Checking)]
:::
