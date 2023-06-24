---
tip: translate by openai@2023-06-23 17:03:11
...
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

> 就像为其他语言所做的一样，GDB为Ada做出了一些通用的扩展（请参见[表达式](Expressions.html#Expressions)）：


- If the expression `E`-1 adjacent variables following it in memory as an array. In Ada, this operator is generally not necessary, since its prime use is in displaying parts of an array, and slicing will usually do this in Ada. However, there are occasional uses when debugging programs in which certain debugging information has been optimized away.

> 如果表达式`E`-1在内存中具有相邻变量，则在Ada中通常不需要此操作符，因为它的主要用途是显示数组的一部分，而slicing通常可以在Ada中完成此操作。但是，在调试某些已优化掉某些调试信息的程序时，有时会有特殊用途。

- `B::var` means "the variable named `var` is a file name, you must typically surround it in single quotes.

> `-`B::var`意味着"变量名为`var`的是一个文件名，通常需要用单引号括起来。`
- The expression `."

- A name starting with '`$`' is a convenience variable (see [Convenience Vars](Convenience-Vars.html#Convenience-Vars)) or a machine register (see [Registers](Registers.html#Registers)).

> 一个以'$'开头的名称是一个便捷变量（参见[便捷变量](Convenience-Vars.html#Convenience-Vars))或机器寄存器（参见[寄存器](Registers.html#Registers)）。


In addition, [GDB] provides a few other shortcuts and outright additions specific to Ada:

> 此外，[GDB]为Ada提供了一些其他的快捷键和直接添加的功能：


- The assignment statement is allowed as an expression, returning its right-hand operand as its value. Thus, you may enter

> 赋值语句可以作为表达式使用，返回其右侧操作数作为其值。因此，您可以输入

  ::: smallexample

  ```bash
  (gdb) set x := y + 3
  (gdb) print A(tmp := y + 1)
  ```

  :::

- The semicolon is allowed as an "operator," returning as its value the value of its right-hand operand. This allows, for example, complex conditional breaks:

> 分号可以作为“操作符”使用，返回其右侧操作数的值。这样就可以实现复杂的条件中断，例如：

  ::: smallexample

  ```bash
  (gdb) break f
  (gdb) condition 1 (report(i); k += 1; A(k) > 100)
  ```

  :::

- An extension to based literals can be used to specify the exact byte contents of a floating-point literal. After the base, you can use from zero to two '`l`' characters controls the width of the resulting real constant: zero means `Float` is used, one means `Long_Float`, and two means `Long_Long_Float`.

> 可以使用扩展的基础文字来指定浮点文字的确切字节内容。在基础之后，您可以使用从零到两个`l`字符来控制生成的实数常量的宽度：零表示使用`Float`，一表示`Long_Float`，两表示`Long_Long_Float`。

  ::: smallexample

  ```bash
  (gdb) print 16f#41b80000#
  $1 = 23.0
  ```

  :::

- Rather than use catenation and symbolic character names to introduce special characters into strings, one may instead use a special bracket notation, which is also used to print strings. A sequence of characters of the form '`["XX"]`' also denotes a single quotation mark in strings. For example,

> 相比起使用连接和符号字符名称将特殊字符引入字符串，还可以使用特殊括号符号，这也用于打印字符串。形式为“[“XX”]”的字符序列也代表字符串中的单引号。例如，

  ::: smallexample

  ```bash
     "One line.["0a"]Next line.["0a"]"
  ```

  :::


  contains an ASCII newline character (`Ada.Characters.Latin_1.LF`) after each period.

> 每句句末都包含一个 ASCII 换行符（`Ada.Characters.Latin_1.LF`）。

- The subtype used as a prefix for the attributes \'Pos, \'Min, and \'Max is optional (and is ignored in any case). For example, it is valid to write

> 这些属性'Pos，'Min和'Max的前缀使用的子类型是可选的（无论如何都会被忽略）。例如，写入是有效的。

  ::: smallexample

  ```bash
  (gdb) print 'max(x, y)
  ```

  :::

- When printing arrays, [GDB] uses positional notation when the array has a lower bound of 1, and uses a modified named notation otherwise. For example, a one-dimensional array of three integers with a lower bound of 3 might print as

> 当打印数组时，[GDB]在数组的下界为1时使用位置符号法，否则使用修改后的命名符号法。例如，一个下界为3的三个整数的一维数组可能会打印为

  ::: smallexample

  ```bash
  (3 => 10, 17, 1)
  ```

  :::


  That is, in contrast to valid Ada, only the first component has a `=>` clause.

> 这就是说，与有效的Ada相比，只有第一个组件有一个`=>`子句。

- You may abbreviate attributes in expressions with any unique, multi-character subsequence of their names (an exact match gets preference). For example, you may use a\'len, a\'gth, or a\'lh in place of a\'length.

> 你可以用属性的任何唯一的、多字符的子序列（精确匹配优先）来缩写表达式中的属性。例如，你可以用a'len、a'gth或a'lh代替a'length。

- Since Ada is case-insensitive, the debugger normally maps identifiers you type to lower case. The GNAT compiler uses upper-case characters for some of its internal identifiers, which are normally of no interest to users. For the rare occasions when you actually have to look at them, enclose them in angle brackets to avoid the lower-case mapping. For example,

> 由于Ada是不区分大小写的，因此调试器通常会将您输入的标识符映射到小写字母。GNAT编译器对其内部标识符使用大写字符，这些标识符通常对用户没有兴趣。在极少数情况下，当您实际上必须查看它们时，请将它们括在尖括号中以避免映射到小写字母。例如，

::: smallexample

```bash
(gdb) print <JMPBUF_SAVE>[0]
```

:::


- Printing an object of class-wide type or dereferencing an access-to-class-wide value will display all the components of the object's specific type (as indicated by its run-time tag). Likewise, component selection on such a value will operate on the specific type of the object.

> 打印类型宽泛的对象或解引用类型宽泛的访问值将显示对象特定类型的所有组件（由其运行时标签指示）。同样，对这样的值进行组件选择将对对象的特定类型进行操作。

---

::: header
Next: [Overloading support for Ada](Overloading-support-for-Ada.html#Overloading-support-for-Ada)]
:::
