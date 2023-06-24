---
tip: translate by openai@2023-06-23 20:13:06
...
---
description: Data (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Data (Debugging with GDB)
lang: en
resource-type: document
title: Data (Debugging with GDB)
---
::: header
Next: [Optimized Code](Optimized-Code.html#Optimized-Code)]
:::

---

## 10 Examining Data


The usual way to examine data in your program is with the `print` command (abbreviated `p`), or its synonym `inspect`. It evaluates and prints the value of an expression of the language your program is written in (see [Using [GDB] with Different Languages](Languages.html#Languages)). It may also print the expression using a Python-based pretty-printer (see [Pretty Printing](Pretty-Printing.html#Pretty-Printing)).

> 通常检查程序中的数据的方法是使用`print`命令（缩写为`p`）或其同义词`inspect`。它会评估并打印程序所使用语言的表达式的值（参见[使用[GDB]与不同语言](Languages.html#Languages))。它也可能使用基于Python的格式化程序打印表达式（参见[格式化输出](Pretty-Printing.html#Pretty-Printing))。

`print [[options] --] expr`
`print [[options] --] /f expr`


:   `expr` is a letter specifying the format; see [Output Formats](Output-Formats.html#Output-Formats).

> `expr` 是一个指定格式的信号；请参见[输出格式](Output-Formats.html#Output-Formats)。

```


The `print` command supports a number of options that allow overriding relevant global print settings as set by `set print` subcommands:

`-address [on`\|`off`]

:   Set printing of addresses. Related setting: [set print address](Print-Settings.html#set-print-address).

`-array [on`\|`off`]

:   Pretty formatting of arrays. Related setting: [set print array](Print-Settings.html#set-print-array).

`-array-indexes [on`\|`off`]

:   Set printing of array indexes. Related setting: [set print array-indexes](Print-Settings.html#set-print-array_002dindexes).

`-characters number-of-characters|elements`\|`unlimited`

:   Set limit on string characters to print. The value `elements` causes the limit on array elements to print to be used. The value `unlimited` causes there to be no limit. Related setting: [set print characters](Print-Settings.html#set-print-characters).

`-elements number-of-elements|unlimited`

:   Set limit on array elements and optionally string characters to print. See [set print characters](Print-Settings.html#set-print-characters), and the `-characters` option above for when this option applies to strings. The value `unlimited` causes there to be no limit. See [set print elements](Print-Settings.html#set-print-elements), for a related CLI command.

`-max-depth depth|unlimited`

:   Set the threshold after which nested structures are replaced with ellipsis. Related setting: [set print max-depth](Print-Settings.html#set-print-max_002ddepth).

`-nibbles [on`\|`off`]

:   Set whether to print binary values in groups of four bits, known as "nibbles". See [set print nibbles](Print-Settings.html#set-print-nibbles).

`-memory-tag-violations [on`\|`off`]

:   Set printing of additional information about memory tag violations. See [set print memory-tag-violations](Print-Settings.html#set-print-memory_002dtag_002dviolations).

`-null-stop [on`\|`off`]

:   Set printing of char arrays to stop at first null char. Related setting: [set print null-stop](Print-Settings.html#set-print-null_002dstop).

`-object [on`\|`off`]

:   Set printing C++ virtual function tables. Related setting: [set print object](Print-Settings.html#set-print-object).

`-pretty [on`\|`off`]

:   Set pretty formatting of structures. Related setting: [set print pretty](Print-Settings.html#set-print-pretty).

`-raw-values [on`\|`off`]

:   Set whether to print values in raw form, bypassing any pretty-printers for that value. Related setting: [set print raw-values](Print-Settings.html#set-print-raw_002dvalues).

`-repeats number-of-repeats|unlimited`

:   Set threshold for repeated print elements. `unlimited` causes all elements to be individually printed. Related setting: [set print repeats](Print-Settings.html#set-print-repeats).

`-static-members [on`\|`off`]

:   Set printing C++ static members. Related setting: [set print static-members](Print-Settings.html#set-print-static_002dmembers).

`-symbol [on`\|`off`]

:   Set printing of symbol names when printing pointers. Related setting: [set print symbol](Print-Settings.html#set-print-symbol).

`-union [on`\|`off`]

:   Set printing of unions interior to structures. Related setting: [set print union](Print-Settings.html#set-print-union).

`-vtbl [on`\|`off`]

:   Set printing of C++ virtual function tables. Related setting: [set print vtbl](Print-Settings.html#set-print-vtbl).

Because the `print` command accepts arbitrary expressions which may look like options (including abbreviations), if you specify any command option, then you must use a double dash (`--`) to mark the end of option processing.

For example, this prints the value of the `-p` expression:

::: smallexample
``` smallexample
(gdb) print -p
```

:::

While this repeats the last value in the value history (see below) with the `-pretty` option in effect:

::: smallexample

```bash
(gdb) print -p --
```

:::

Here is an example including both on option and an expression:

::: smallexample

```bash
(gdb) print -pretty -- *myptr
$1 = {
  next = 0x0,
  flags = {
    sweet = 1,
    sour = 1
  },
  meat = 0x54 "Pork"
}
```

:::

```

`print [options]`
`print [options] /f`

:   

```

If you omit `expr` displays the last value again (from the *value history*; see [Value History](Value-History.html#Value-History)). This allows you to conveniently inspect the same value in an alternative format.

```


If the architecture supports memory tagging, the `print` command will display pointer/memory tag mismatches if what is being printed is a pointer or reference type. See [Memory Tagging](Memory-Tagging.html#Memory-Tagging).

> 如果架构支持内存标记，则如果正在打印的是指针或引用类型，则`print`命令将显示指针/内存标记不匹配。参见[内存标记](Memory-Tagging.html#Memory-Tagging)。


A more low-level way of examining data is with the `x` command. It examines data in memory at a specified address and prints it in a specified format. See [Examining Memory](Memory.html#Memory).

> 一种更低级别的检查数据的方法是使用`x`命令。它在指定地址检查内存中的数据，并以指定格式打印它。参见[检查内存](Memory.html#Memory)。


If you are interested in information about types, or about how the fields of a struct or a class are declared, use the `ptype expr` command rather than `print`. See [Examining the Symbol Table](Symbols.html#Symbols).

> 如果您有兴趣了解有关类型的信息或有关如何声明结构或类的字段，请使用`ptype expr`命令而不是`print`。请参见[检查符号表](Symbols.html#Symbols)。




Another way of examining values of expressions and type information is through the Python extension command `explore` (available only if the [GDB] build is configured with `--with-python`). It offers an interactive way to start at the highest level (or, the most abstract level) of the data type of an expression (or, the data type itself) and explore all the way down to leaf scalar values/fields embedded in the higher level data types.

> 另一种检查表达式值和类型信息的方法是通过Python扩展命令`explore`（仅当使用`--with-python`配置[GDB]时可用）。它提供了一种交互式的方式，从表达式（或数据类型本身）的最高级别（或最抽象级别）开始，探索一直到嵌入在较高级数据类型中的叶子标量值/字段。

`explore arg`


:   `arg` is either an expression (in the source language), or a type visible in the current context of the program being debugged.

> `arg` 是一个表达式（在源语言中），或者是当前调试程序上下文中可见的类型。


The working of the `explore` command can be illustrated with an example. If a data type `struct ComplexStruct` is defined in your C program as

> 实例可以说明`explore`命令的工作原理。如果在C程序中定义了数据类型`struct ComplexStruct`，

::: smallexample

```bash
struct SimpleStruct
{
  int i;
  double d;
};

struct ComplexStruct
{
  struct SimpleStruct *ss_p;
  int arr[10];
};
```

:::

followed by variable declarations as

::: smallexample

```bash
struct SimpleStruct ss = ;
struct ComplexStruct cs = ;
```

:::


then, the value of the variable `cs` can be explored using the `explore` command as follows.

> 然后，可以使用“探索”命令来探索变量`cs`的值。

::: smallexample

```bash
(gdb) explore cs
The value of `cs' is a struct/class of type `struct ComplexStruct' with
the following fields:

  ss_p = <Enter 0 to explore this field of type `struct SimpleStruct *'>
   arr = <Enter 1 to explore this field of type `int [10]'>

Enter the field number of choice:
```

:::


Since the fields of `cs` are not scalar values, you are being prompted to chose the field you want to explore. Let's say you choose the field `ss_p` by entering `0`. Then, since this field is a pointer, you will be asked if it is pointing to a single value. From the declaration of `cs` above, it is indeed pointing to a single value, hence you enter `y`. If you enter `n`, then you will be asked if it were pointing to an array of values, in which case this field will be explored as if it were an array.

> 由于`cs`的字段不是标量值，您被提示选择要探索的字段。假设您通过输入`0`选择了`ss_p`字段。然后，由于此字段是指针，您将被要求确定它是否指向单个值。从上面的`cs`声明中，它确实指向单个值，因此您输入`y`。如果您输入`n`，则会询问它是否指向一组值，在这种情况下，此字段将被视为数组进行探索。

::: smallexample

```bash
`cs.ss_p' is a pointer to a value of type `struct SimpleStruct'
Continue exploring it as a pointer to a single value [y/n]: y
The value of `*(cs.ss_p)' is a struct/class of type `struct
SimpleStruct' with the following fields:

  i = 10 .. (Value of type `int')
  d = 1.1100000000000001 .. (Value of type `double')

Press enter to return to parent value:
```

:::


If the field `arr` of `cs` was chosen for exploration by entering `1` earlier, then since it is as array, you will be prompted to enter the index of the element in the array that you want to explore.

> 如果之前通过输入“1”选择了“cs”中的“arr”字段进行探索，那么由于它是一个数组，您将被提示输入您想探索的数组元素的索引。

::: smallexample

```bash
`cs.arr' is an array of `int'.
Enter the index of the element you want to explore in `cs.arr': 5

`(cs.arr)[5]' is a scalar value of type `int'.

(cs.arr)[5] = 4

Press enter to return to parent value: 
```

:::


In general, at any stage of exploration, you can go deeper towards the leaf values by responding to the prompts appropriately, or hit the return key to return to the enclosing data structure (the *higher* level data structure).

> 一般来说，在任何探索阶段，您都可以通过适当地回答提示来深入探索叶值，或者按回车键返回到包含数据结构（更高级别的数据结构）。


Similar to exploring values, you can use the `explore` command to explore types. Instead of specifying a value (which is typically a variable name or an expression valid in the current context of the program being debugged), you specify a type name. If you consider the same example as above, your can explore the type `struct ComplexStruct` by passing the argument `struct ComplexStruct` to the `explore` command.

> 类似于探索值，您可以使用“explore”命令来探索类型。而不是指定值（通常是变量名或调试程序当前上下文中有效的表达式），您指定类型名称。如果您考虑相同的示例，您可以通过将参数“struct ComplexStruct”传递给“explore”命令来探索类型“struct ComplexStruct”。

::: smallexample

```bash
(gdb) explore struct ComplexStruct
```

:::


By responding to the prompts appropriately in the subsequent interactive session, you can explore the type `struct ComplexStruct` in a manner similar to how the value `cs` was explored in the above example.

> 回答下一個交互式會話中的提示，您可以以與上面例子中對cs的探索方式類似的方式來探索類型'struct ComplexStruct'。


The `explore` command also has two sub-commands, `explore value` and `explore type`. The former sub-command is a way to explicitly specify that value exploration of the argument is being invoked, while the latter is a way to explicitly specify that type exploration of the argument is being invoked.

> 命令`explore`也有两个子命令，`explore value`和`explore type`。前者是明确指定调用参数的值探索的方式，而后者是明确指定调用参数的类型探索的方式。

`explore value expr`

:

```
This sub-command of `explore` explores the value of the expression `expr`.
```

`explore type arg`

:

```
This sub-command of `explore` explores the type of `arg` as the argument.
```

---


• [Expressions](Expressions.html#Expressions):                                      Expressions

> • 表达式（Expressions.html#Expressions）：表达式

• [Ambiguous Expressions](Ambiguous-Expressions.html#Ambiguous-Expressions):        Ambiguous Expressions

> • [模糊表述](Ambiguous-Expressions.html#Ambiguous-Expressions):    模糊表述

• [Variables](Variables.html#Variables):                                            Program variables

> • [变量](Variables.html#Variables):               程序变量

• [Arrays](Arrays.html#Arrays):                                                     Artificial arrays

> • [阵列](Arrays.html#Arrays):                                                     人造阵列

• [Output Formats](Output-Formats.html#Output-Formats):                             Output formats

> • [输出格式](Output-Formats.html#Output-Formats):                             输出格式

• [Memory](Memory.html#Memory):                                                     Examining memory

> • [内存](Memory.html#Memory)：检查内存

• [Memory Tagging](Memory-Tagging.html#Memory-Tagging):                             Memory Tagging

> • [内存标记](Memory-Tagging.html#Memory-Tagging)：内存标记

• [Auto Display](Auto-Display.html#Auto-Display):                                   Automatic display

> • [自动显示](Auto-Display.html#Auto-Display):                                 自动显示

• [Print Settings](Print-Settings.html#Print-Settings):                             Print settings

> • [打印设置](Print-Settings.html#Print-Settings)：打印设置

• [Pretty Printing](Pretty-Printing.html#Pretty-Printing):                                         Python pretty printing

> • [格式化输出](Pretty-Printing.html#Pretty-Printing):                                 Python格式化输出

• [Value History](Value-History.html#Value-History):                                               Value history

> • [价值历史](Value-History.html#Value-History): 追踪价值历史

• [Convenience Vars](Convenience-Vars.html#Convenience-Vars):                                      Convenience variables

> • [便利变量](Convenience-Vars.html#Convenience-Vars):                                      便利变量

• [Convenience Funs](Convenience-Funs.html#Convenience-Funs):                                      Convenience functions

> • [便利功能](Convenience-Funs.html#Convenience-Funs):        便利函数

• [Registers](Registers.html#Registers):                                                           Registers

> • [注册](Registers.html#Registers): 注册

• [Floating Point Hardware](Floating-Point-Hardware.html#Floating-Point-Hardware):                 Floating point hardware

> • [浮点硬件](Floating-Point-Hardware.html#Floating-Point-Hardware):                 浮点硬件

• [Vector Unit](Vector-Unit.html#Vector-Unit):                                                     Vector Unit

> • [向量单位](Vector-Unit.html#Vector-Unit):                                                     向量单位

• [OS Information](OS-Information.html#OS-Information):                                            Auxiliary data provided by operating system

> • [操作系统信息](OS-Information.html#OS-Information): 由操作系统提供的辅助数据

• [Memory Region Attributes](Memory-Region-Attributes.html#Memory-Region-Attributes):              Memory region attributes

> • [内存区域属性](Memory-Region-Attributes.html#Memory-Region-Attributes):              内存区域属性

• [Dump/Restore Files](Dump_002fRestore-Files.html#Dump_002fRestore-Files):                        Copy between memory and a file

> • [备份/恢复文件](Dump_002fRestore-Files.html#Dump_002fRestore-Files):                        在内存和文件之间复制

• [Core File Generation](Core-File-Generation.html#Core-File-Generation):                          Cause a program dump its core

> • [生成核心文件](Core-File-Generation.html#Core-File-Generation)：使程序转储其核心文件

• [Character Sets](Character-Sets.html#Character-Sets):                                            Debugging programs that use a different character set than GDB does

> •[字符集](Character-Sets.html#Character-Sets):                           调试使用与GDB不同字符集的程序。

• [Caching Target Data](Caching-Target-Data.html#Caching-Target-Data):                             Data caching for targets

> • [缓存目标数据](Caching-Target-Data.html#Caching-Target-Data):                             为目标缓存数据

• [Searching Memory](Searching-Memory.html#Searching-Memory):                                      Searching memory for a sequence of bytes

> • [搜索記憶](Searching-Memory.html#Searching-Memory):  搜索記憶以尋找一系列位元組

• [Value Sizes](Value-Sizes.html#Value-Sizes):                                                     Managing memory allocated for values

> •[值大小](Value-Sizes.html#Value-Sizes)：管理分配给值的内存

---

---

::: header
Next: [Optimized Code](Optimized-Code.html#Optimized-Code)]
:::
