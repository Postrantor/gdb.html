---
description: Additions to Ada (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Additions to Ada (Debugging with GDB)
lang: en
resource-type: document
title: Additions to Ada (Debugging with GDB)
---
::: header
Next: [Overloading support for Ada](Overloading-support-for-Ada.html#Overloading-support-for-Ada)]
:::

---

#### 15.4.10.3 Additions to Ada

As it does for other languages, [GDB] makes certain generic extensions to Ada (see [Expressions](Expressions.html#Expressions)):

- If the expression `E`-1 adjacent variables following it in memory as an array. In Ada, this operator is generally not necessary, since its prime use is in displaying parts of an array, and slicing will usually do this in Ada. However, there are occasional uses when debugging programs in which certain debugging information has been optimized away.
- `B::var` means "the variable named `var` is a file name, you must typically surround it in single quotes.
- The expression `."
- A name starting with '`$`' is a convenience variable (see [Convenience Vars](Convenience-Vars.html#Convenience-Vars)) or a machine register (see [Registers](Registers.html#Registers)).

In addition, [GDB] provides a few other shortcuts and outright additions specific to Ada:

- The assignment statement is allowed as an expression, returning its right-hand operand as its value. Thus, you may enter

  ::: smallexample

  ```bash
  (gdb) set x := y + 3
  (gdb) print A(tmp := y + 1)
  ```

  :::
- The semicolon is allowed as an "operator," returning as its value the value of its right-hand operand. This allows, for example, complex conditional breaks:

  ::: smallexample

  ```bash
  (gdb) break f
  (gdb) condition 1 (report(i); k += 1; A(k) > 100)
  ```

  :::
- An extension to based literals can be used to specify the exact byte contents of a floating-point literal. After the base, you can use from zero to two '`l`' characters controls the width of the resulting real constant: zero means `Float` is used, one means `Long_Float`, and two means `Long_Long_Float`.

  ::: smallexample

  ```bash
  (gdb) print 16f#41b80000#
  $1 = 23.0
  ```

  :::
- Rather than use catenation and symbolic character names to introduce special characters into strings, one may instead use a special bracket notation, which is also used to print strings. A sequence of characters of the form '`["XX"]`' also denotes a single quotation mark in strings. For example,

  ::: smallexample

  ```bash
     "One line.["0a"]Next line.["0a"]"
  ```

  :::

  contains an ASCII newline character (`Ada.Characters.Latin_1.LF`) after each period.
- The subtype used as a prefix for the attributes \'Pos, \'Min, and \'Max is optional (and is ignored in any case). For example, it is valid to write

  ::: smallexample

  ```bash
  (gdb) print 'max(x, y)
  ```

  :::
- When printing arrays, [GDB] uses positional notation when the array has a lower bound of 1, and uses a modified named notation otherwise. For example, a one-dimensional array of three integers with a lower bound of 3 might print as

  ::: smallexample

  ```bash
  (3 => 10, 17, 1)
  ```

  :::

  That is, in contrast to valid Ada, only the first component has a `=>` clause.
- You may abbreviate attributes in expressions with any unique, multi-character subsequence of their names (an exact match gets preference). For example, you may use a\'len, a\'gth, or a\'lh in place of a\'length.
- Since Ada is case-insensitive, the debugger normally maps identifiers you type to lower case. The GNAT compiler uses upper-case characters for some of its internal identifiers, which are normally of no interest to users. For the rare occasions when you actually have to look at them, enclose them in angle brackets to avoid the lower-case mapping. For example,

::: smallexample

```bash
(gdb) print <JMPBUF_SAVE>[0]
```

:::

- Printing an object of class-wide type or dereferencing an access-to-class-wide value will display all the components of the object's specific type (as indicated by its run-time tag). Likewise, component selection on such a value will operate on the specific type of the object.

---

::: header
Next: [Overloading support for Ada](Overloading-support-for-Ada.html#Overloading-support-for-Ada)]
:::
