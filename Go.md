---
tip: translate by openai@2023-06-23 22:57:10
...
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

> 不需要指定当前包的名称时，指定全局变量和函数。

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

> 解析器GDB表达式认识`unsafe.Sizeof`函数并由它自行处理。

`Restrictions on Go expressions`


All Go operators are supported except `&^`. The Go `_` "blank identifier" is not supported. Automatic dereferencing of pointers is not supported.

> 所有Go操作符都支持，除了`&^`。Go的`_`“空标识符”不受支持。不支持自动取消指针的引用。
