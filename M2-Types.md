---
tip: translate by openai@2023-06-24 10:27:42
...
---
description: M2 Types (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: M2 Types (Debugging with GDB)
lang: en
resource-type: document
title: M2 Types (Debugging with GDB)
---
::: header
Next: [M2 Defaults](M2-Defaults.html#M2-Defaults)]
:::

---

#### 15.4.9.4 Modula-2 Types

Currently [GDB] sessions.

The first example contains the following section of code:

::: smallexample

```bash
VAR
   s: SET OF CHAR ;
   r: [20..40] ;
```

:::


and you can request [GDB] to interrogate the type and value of `r` and `s`.

> 你可以要求GDB查询`r`和`s`的类型和值。

::: smallexample

```bash
(gdb) print s

(gdb) ptype s
SET OF CHAR
(gdb) print r
21
(gdb) ptype r
[20..40]
```

:::

Likewise if your source code declares `s` as:

::: smallexample

```bash
VAR
   s: SET ['A'..'Z'] ;
```

:::

then you may query the type of `s` by:

::: smallexample

```bash
(gdb) ptype s
type = SET ['A'..'Z']
```

:::


Note that at present you cannot interactively manipulate set expressions using the debugger.

> 目前，您无法使用调试器交互式地操作集合表达式。


The following example shows how you might declare an array in Modula-2 and how you can interact with [GDB] to print its type and contents:

> 以下示例展示了如何在Modula-2中声明数组，以及如何使用[GDB]打印其类型和内容：

::: smallexample

```bash
VAR
   s: ARRAY [-10..10] OF CHAR ;
```

:::

::: smallexample

```bash
(gdb) ptype s
ARRAY [-10..10] OF CHAR
```

:::


Note that the array handling is not yet complete and although the type is printed correctly, expression handling still assumes that all arrays have a lower bound of zero and not `-10` as in the example above.

> 注意，数组处理尚未完成，尽管类型正确地打印出来了，但表达式处理仍然假定所有数组的下界都是零，而不是上面示例中的`-10`。

Here are some more type related Modula-2 examples:

::: smallexample

```bash
TYPE
   colour = (blue, red, yellow, green) ;
   t = [blue..yellow] ;
VAR
   s: t ;
BEGIN
   s := blue ;
```

:::


The [GDB] interaction shows how you can query the data type and value of a variable.

> 交互式调试器（GDB）展示了如何查询变量的数据类型和值。

::: smallexample

```bash
(gdb) print s
$1 = blue
(gdb) ptype t
type = [blue..yellow]
```

:::


In this example a Modula-2 array is declared and its contents displayed. Observe that the contents are written in the same way as their `C` counterparts.

> 在这个例子中，声明了一个Modula-2数组，并显示了其内容。请注意，内容的书写方式与其`C`对应物完全相同。

::: smallexample

```bash
VAR
   s: ARRAY [1..5] OF CARDINAL ;
BEGIN
   s[1] := 1 ;
```

:::

::: smallexample

```bash
(gdb) print s
$1 = 
(gdb) ptype s
type = ARRAY [1..5] OF CARDINAL
```

:::


The Modula-2 language interface to [GDB] also understands pointer types as shown in this example:

> 模块2语言接口到[GDB]也理解指针类型，如下例所示：

::: smallexample

```bash
VAR
   s: POINTER TO ARRAY [1..5] OF CARDINAL ;
BEGIN
   NEW(s) ;
   s^[1] := 1 ;
```

:::

and you can request that [GDB] describes the type of `s`.

::: smallexample

```bash
(gdb) ptype s
type = POINTER TO ARRAY [1..5] OF CARDINAL
```

:::


[GDB] handles compound types as we can see in this example. Here we combine array types, record types, pointer types and subrange types:

> GDB可以处理复合类型，如本例所示。这里我们结合了数组类型、记录类型、指针类型和子范围类型。

::: smallexample

```bash
TYPE
   foo = RECORD
            f1: CARDINAL ;
            f2: CHAR ;
            f3: myarray ;
         END ;

   myarray = ARRAY myrange OF CARDINAL ;
   myrange = [-2..2] ;
VAR
   s: POINTER TO ARRAY myrange OF foo ;
```

:::

and you can ask [GDB] to describe the type of `s` as shown below.

::: smallexample

```bash
(gdb) ptype s
type = POINTER TO ARRAY [-2..2] OF foo = RECORD
    f1 : CARDINAL;
    f2 : CHAR;
    f3 : ARRAY [-2..2] OF CARDINAL;
END 
```

:::

---

::: header
Next: [M2 Defaults](M2-Defaults.html#M2-Defaults)]
:::
