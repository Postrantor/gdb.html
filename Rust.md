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

- Linespecs (see [Location Specifications](Location-Specifications.html#Location-Specifications)) are never relative to the current crate. Instead, they act as if there were a global namespace of crates, somewhat similar to the way `extern crate` behaves.

  That is, if [GDB]'.

  As a consequence of this approach, linespecs also cannot refer to items using '`self::`'.
- Because [GDB]'.

  However, since it is useful to be able to refer to other crates when debugging, [GDB] provides the `extern` extension to circumvent this. To use the extension, just put `extern` before a path expression to refer to the otherwise unavailable "global" scope.

  In the above example, if you wanted to refer to the symbol '`y`', you would use `print extern x::y`.
- The Rust expression evaluator does not support "statement-like" expressions such as `if` or `match`, or lambda expressions.
- Tuple expressions are not implemented.
- The Rust expression evaluator does not currently implement the `Drop` trait. Objects that may be created by the evaluator will never be destroyed.
- [GDB] does not implement type inference for generics. In order to call generic functions or otherwise refer to generic items, you will have to specify the type parameters manually.
- [GDB] might provide a completion like `crate::f<u32>`, where the parser would require `crate::f::<u32>`.
- As of this writing, the Rust compiler (version 1.8) has a few holes in the debugging information it generates. These holes prevent certain features from being implemented by [GDB]:

  - Method calls cannot be made via traits.
  - Operator overloading is not implemented.
  - When debugging in a monomorphized function, you cannot use the generic type names.
  - The type `Self` is not available.
  - `use` statements are not available, so some names may not be available in the crate.

---

::: header
Next: [Modula-2](Modula_002d2.html#Modula_002d2)]
:::
