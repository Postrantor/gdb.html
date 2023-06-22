---
description: Go (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Go (Debugging with GDB)
lang: en
resource-type: document
title: Go (Debugging with GDB)
---
::: header
Next: [Objective-C](Objective_002dC.html#Objective_002dC)]
:::

---

#### 15.4.3 Go

[GDB] compilers.

Here is a summary of the Go-specific features and restrictions:

`The current Go package`

The name of the current package does not need to be specified when specifying global variables and functions.

For example, given the program:

::: example

```example
package main
var myglob = "Shall we?"
func main () {
  // ...
}
```

:::

When stopped inside `main` either of these work:

::: example

```example
(gdb) p myglob
(gdb) p main.myglob
```

:::

`Builtin Go types`

The `string` type is recognized by [GDB] and is printed as a string.

`Builtin Go functions`

The [GDB] expression parser recognizes the `unsafe.Sizeof` function and handles it internally.

`Restrictions on Go expressions`

All Go operators are supported except `&^`. The Go `_` "blank identifier" is not supported. Automatic dereferencing of pointers is not supported.
