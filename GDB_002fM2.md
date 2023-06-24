---
tip: translate by openai@2023-06-23 21:42:17
...
---
description: GDB/M2 (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: GDB/M2 (Debugging with GDB)
lang: en
resource-type: document
title: GDB/M2 (Debugging with GDB)
---
::: header
Previous: [M2 Scope](M2-Scope.html#M2-Scope)]
:::

---

#### 15.4.9.9 [GDB]


Some [GDB]'. The first four apply to C++, and the last to the C `union` type, which has no direct analogue in Modula-2.

> 一些[GDB]。前四个适用于C++，最后一个适用于C语言的`union`类型，Modula-2没有直接等价物。


The `@` operator (see [Expressions](Expressions.html#Expressions)), while available with any language, is not useful with Modula-2. Its intent is to aid the debugging of *dynamic arrays*, which cannot be created in Modula-2 as they can in C or C++. However, because an address can be specified by an integral constant, the construct '`' is still useful.

> @操作符（参见[表达式](Expressions.html#Expressions））虽然可以在任何语言中使用，但在Modula-2中却没有用处。它的目的是帮助调试动态数组，而这在Modula-2中是不可能实现的，但在C或C++中却可以实现。然而，由于可以通过整数常量指定地址，因此构造'`'仍然很有用。


In [GDB] scripts, the Modula-2 inequality operator `#` is interpreted as the beginning of a comment. Use `<>` instead.

> 在GDB脚本中，Modula-2不等式操作符'#'被解释为注释的开头。请使用'<>'代替。
