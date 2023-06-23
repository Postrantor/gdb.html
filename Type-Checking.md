---
description: Type Checking (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Type Checking (Debugging with GDB)
lang: en
resource-type: document
title: Type Checking (Debugging with GDB)
---
::: header
Next: [Range Checking](Range-Checking.html#Range-Checking)]
:::

---

#### 15.3.1 An Overview of Type Checking

Some languages, such as C and C++, are strongly typed, meaning that the arguments to operators and functions have to be of the correct type, otherwise an error occurs. These checks prevent type mismatch errors from ever causing any run-time problems. For example,

::: smallexample

```bash
int klass::my_method(char *b) 

(gdb) print obj.my_method (0)
$1 = 2
```

```bash
but
```

```bash
(gdb) print obj.my_method (0x1234)
Cannot resolve method klass::my_method to any overloaded instance
```

:::

The second example fails because in C++ the integer constant '`0x1234`' is not type-compatible with the pointer parameter type.

For the expressions you use in [GDB] successfully evaluates expressions like the second example above.

Even if type checking is off, there may be other reasons related to type that prevent [GDB] does not know how to add an `int` and a `struct foo`. These particular type errors have nothing to do with the language in use and usually arise from expressions which make little sense to evaluate anyway.

[GDB] provides some additional commands for controlling type checking:

`set check type on`
`set check type off`

:   Set strict type checking on or off. If any type mismatches occur in evaluating an expression while type checking is on, [GDB] prints a message and aborts evaluation of the expression.

`show check type`

:   Show the current setting of type checking and whether [GDB] is enforcing strict type checking rules.

---

::: header
Next: [Range Checking](Range-Checking.html#Range-Checking)]
:::
