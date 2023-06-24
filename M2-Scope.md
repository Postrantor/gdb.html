---
tip: translate by openai@2023-06-24 10:27:28
...
---
description: M2 Scope (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: M2 Scope (Debugging with GDB)
lang: en
resource-type: document
title: M2 Scope (Debugging with GDB)
---
::: header
Next: [GDB/M2](GDB_002fM2.html#GDB_002fM2)]
:::

---

#### 15.4.9.8 The Scope Operators `::` and `.`


There are a few subtle differences between the Modula-2 scope operator (`.`) and the [GDB] scope operator (`::`). The two have similar syntax:

> 在Modula-2的作用域运算符（“。”）和[GDB]的作用域运算符（“::”）之间存在一些微妙的差异。两者的语法相似：

::: smallexample

```bash
module . id
scope :: id
```

:::


where `scope` is any declared identifier within your program, except another module.

> 在程序中，`scope`是指任何声明的标识符，除了另一个模块之外。

Using the `::` operator makes [GDB].

Using the `.` operator makes [GDB].
