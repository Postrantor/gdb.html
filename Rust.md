---
tip: translate by openai@2023-06-23 12:32:46
...
---
description: Rust (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Rust (Debugging with GDB)
lang: en
resource-type: document
title: Rust (Debugging with GDB)
---
::: header
Next: [Modula-2](Modula_002d2.html#Modula_002d2)]
:::

---

#### 15.4.8 Rust


[GDB] supports the [Rust Programming Language](https://www.rust-lang.org/). Type- and value-printing, and expression parsing, are reasonably complete. However, there are a few peculiarities and holes to be aware of.

> [GDB]支持[Rust编程语言](https://www.rust-lang.org/)。类型和值打印以及表达式解析相当完整。但是，需要注意一些特殊情况和缺陷。


- Linespecs (see [Location Specifications](Location-Specifications.html#Location-Specifications)) are never relative to the current crate. Instead, they act as if there were a global namespace of crates, somewhat similar to the way `extern crate` behaves.

> 行规范（参见[位置规范](Location-Specifications.html#Location-Specifications)）永远不是相对于当前框架的。相反，它们的行为就好像有一个全局的框架名称空间，有点类似于`extern crate`的行为。

  That is, if [GDB]'.


  As a consequence of this approach, linespecs also cannot refer to items using '`self::`'.

> 因此，线路规格也无法使用“self::”引用项目。
- Because [GDB]'.


  However, since it is useful to be able to refer to other crates when debugging, [GDB] provides the `extern` extension to circumvent this. To use the extension, just put `extern` before a path expression to refer to the otherwise unavailable "global" scope.

> 然而，由于在调试时能够引用其他柜台很有用，[GDB]提供了`extern`扩展来解决这个问题。要使用此扩展，只需在路径表达式之前放置`extern`以引用否则不可用的“全局”作用域。


  In the above example, if you wanted to refer to the symbol '`y`', you would use `print extern x::y`.

> 在上面的例子中，如果你想引用符号'y'，你可以使用`print extern x::y`。

- The Rust expression evaluator does not support "statement-like" expressions such as `if` or `match`, or lambda expressions.

> Rust表达式求值器不支持像`if`或`match`这样的“语句类”表达式或lambda表达式。
- Tuple expressions are not implemented.

- The Rust expression evaluator does not currently implement the `Drop` trait. Objects that may be created by the evaluator will never be destroyed.

> 评估器中的Rust表达式目前尚未实现`Drop`特性。由评估器创建的对象永远不会被销毁。
- [GDB] does not implement type inference for generics. In order to call generic functions or otherwise refer to generic items, you will have to specify the type parameters manually.
- [GDB] might provide a completion like `crate::f<u32>`, where the parser would require `crate::f::<u32>`.

- As of this writing, the Rust compiler (version 1.8) has a few holes in the debugging information it generates. These holes prevent certain features from being implemented by [GDB]:

> 截至目前，Rust编译器（版本1.8）在生成的调试信息中存在一些漏洞。这些漏洞阻止了[GDB]实现某些功能。

  - Method calls cannot be made via traits.
  - Operator overloading is not implemented.
  - When debugging in a monomorphized function, you cannot use the generic type names.
  - The type `Self` is not available.
  - `use` statements are not available, so some names may not be available in the crate.

---

::: header
Next: [Modula-2](Modula_002d2.html#Modula_002d2)]
:::
