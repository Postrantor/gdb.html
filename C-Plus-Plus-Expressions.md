---
description: C Plus Plus Expressions (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: C Plus Plus Expressions (Debugging with GDB)
lang: en
resource-type: document
title: C Plus Plus Expressions (Debugging with GDB)
---
::: header
Next: [C Defaults](C-Defaults.html#C-Defaults)]
:::

---

#### 15.4.1.3 C++ Expressions

[GDB] expression handling can interpret most C++ expressions.

> *Warning:* [GDB] to debug C++ code. See [Compilation](Compilation.html#Compilation).

1. Member function calls are allowed; you can use expressions like

::: smallexample

```bash
count = aml->GetOriginal(x, y)
```

:::
2. .
3.  does not perform overload resolution involving user-defined type conversions, calls to constructors, or instantiations of templates that do not exist in the program. It also cannot handle ellipsis argument lists or default arguments.

It does perform integral conversions and promotions, floating-point promotions, arithmetic conversions, pointer conversions, conversions of class objects to base classes, and standard conversions such as those of functions or arrays to pointers; it requires an exact match on the number of function arguments.

Overload resolution is always performed, unless you have specified `set overload-resolution off`. See [[GDB] Features for C++](Debugging-C-Plus-Plus.html#Debugging-C-Plus-Plus).

You must specify `set overload-resolution off` in order to use an explicit function signature to call an overloaded function, as in

::: smallexample

```bash
p 'foo(char,int)'('x', 13)
```

:::

The [GDB] command-completion facility can simplify this; see [Command Completion](Completion.html#Completion).
4.  understands variables declared as C++ lvalue or rvalue references; you can use them in expressions just as you do in C++ source---they are automatically dereferenced.

In the parameter list shown when [GDB]'.
5. [GDB] also allows resolving name scope by reference to source files, in both C and C++ debugging (see [Program Variables](Variables.html#Variables)).
6. [GDB] performs argument-dependent lookup, following the C++ specification.

---

::: header
Next: [C Defaults](C-Defaults.html#C-Defaults)]
:::
