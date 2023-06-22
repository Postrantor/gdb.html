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

The `@` operator (see [Expressions](Expressions.html#Expressions)), while available with any language, is not useful with Modula-2. Its intent is to aid the debugging of *dynamic arrays*, which cannot be created in Modula-2 as they can in C or C++. However, because an address can be specified by an integral constant, the construct '`' is still useful.

In [GDB] scripts, the Modula-2 inequality operator `#` is interpreted as the beginning of a comment. Use `<>` instead.
