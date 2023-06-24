---
tip: translate by openai@2023-06-24 00:54:37
...
---
description: Output (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Output (Debugging with GDB)
lang: en
resource-type: document
title: Output (Debugging with GDB)
---
::: header
Next: [Auto-loading sequences](Auto_002dloading-sequences.html#Auto_002dloading-sequences)]
:::

---

#### 23.1.4 Commands for Controlled Output


During the execution of a command file or a user-defined command, normal [GDB] output is suppressed; the only output that appears is what is explicitly printed by the commands in the definition. This section describes three commands useful for generating exactly the output you want.

> 在执行命令文件或用户定义的命令时，会抑制普通[GDB]输出；唯一会出现的输出是定义中命令明确打印的内容。本节描述了三个有用的命令，它们可以生成您想要的正确输出。

`echo text`

Print `text`'.


A backslash at the end of `text` can be used, as in C, to continue the command onto subsequent lines. For example,

> 一个反斜杠在文本末尾可以像C语言一样，用来将命令延续到后续行。例如，

::: smallexample

```bash
echo This is some text\n\
which is continued\n\
onto several lines.\n
```

:::

produces the same output as

::: smallexample

```bash
echo This is some text\n
echo which is continued\n
echo onto several lines.\n
```

:::

`output expression`


Print the value of `expression`'. The value is not entered in the value history either. See [Expressions](Expressions.html#Expressions), for more information on expressions.

> 打印表达式的值。该值不在值历史记录中。有关表达式的更多信息，请参阅[表达式](Expressions.html#Expressions)。

`output/fmt expression`


Print the value of `expression`. You can use the same formats as for `print`. See [Output Formats](Output-Formats.html#Output-Formats), for more information.

> 打印表达式的值。您可以使用与`print`相同的格式。有关更多信息，请参阅[输出格式](Output-Formats.html#Output-Formats)。

`printf template, expressions…`


Print the values of one or more `expressions`, exactly as a C program would do by executing the code below:

> 打印一个或多个表达式的值，就像C程序执行下面的代码一样。

::: smallexample

```bash
printf (template, expressions…);
```

:::


As in `C` `printf`, ordinary characters in `template` to be evaluated, their values converted and formatted according to type and style information encoded in the conversion specifications, and then printed.

> 就像在C语言的printf函数中一样，模板中的普通字符会被评估，根据转换规范中编码的类型和样式信息将它们的值转换并格式化，然后输出。

For example, you can print two values in hex like this:

::: smallexample

```bash
printf "foo, bar-foo = 0x%x, 0x%x\n", foo, bar-foo
```

:::

`printf` supports all the standard `C` conversion specifications, including the flags and modifiers between the '`%`' character and the conversion letter, with the following exceptions:

- The argument-ordering modifiers, such as '`2$`', are not supported.
- The modifier '`*`' is not supported for specifying precision or width.

- The '`'`' flag (for separation of digits into groups according to `LC_NUMERIC'`) is not supported.

> 不支持'`'`'标志（按照'LC_NUMERIC'将数字分组）。
- The type modifiers '`hh`' are not supported.
- The conversion letter '`n`') is not supported.
- The conversion letters '`a`' are not supported.


Note that the '`ll`' type modifier is supported only if `long double` type is available.

> 注意，只有在`long double`类型可用时，才支持`ll`类型修饰符。


As in `C`, `printf` supports simple backslash-escape sequences, such as `\n`, '`\t`', that consist of backslash followed by a single character. Octal and hexadecimal escape sequences are not supported.

> 在C语言中，printf函数支持简单的反斜杠转义序列，如\n、\t，它们由反斜杠和单个字符组成。不支持八进制和十六进制转义序列。


Additionally, `printf` supports conversion specifications for DFP (*Decimal Floating Point*) types using the following length modifiers together with a floating point specifier. letters:

> 此外，`printf` 支持使用以下长度修饰符与浮点指定符一起使用的DFP（十进制浮点）类型的转换规范。

- '`H`' for printing `Decimal32` types.
- '`D`' for printing `Decimal64` types.
- '`DD`' for printing `Decimal128` types.

If the underlying `C` implementation used to build [GDB] to use.


In case there is no such `C` support, no additional modifiers will be available and the value will be printed in the standard way.

> 如果没有这种C支持，将不提供额外的修饰符，值将以标准方式输出。


Here's an example of printing DFP types using the above conversion letters:

> 这是使用上述转换字母打印DFP类型的一个例子：

::: smallexample

```bash
printf "D32: %Hf - D64: %Df - D128: %DDf\n",1.2345df,1.2E10dd,1.2E1dl
```

:::


Additionally, `printf` supports a special '`%V` command (see [Examining Data](Data.html#Data)):

> 此外，`printf`支持一个特殊的'`％V`命令（请参见[检查数据](Data.html#Data)）：

::: smallexample

```bash
(gdb) print array
$1 = 
(gdb) printf "Array is: %V\n", array
Array is: 
```

:::

It is possible to include print options with the '`%V`', like this:

::: smallexample

```bash
(gdb) printf "Array is: %V[-array-indexes on]\n", array
Array is: 
```

:::


If you need to print a literal '`[`', then just include an empty print options list:

> 如果你需要打印一个字面上的'[', 那么只需要包含一个空的打印选项列表即可：

::: smallexample

```bash
(gdb) printf "Array is: %V[Hello]\n", array
Array is: [Hello]
```

:::

`eval template, expressions…`


Convert the values of one or more `expressions` to a command line, and call it.

> 将一个或多个表达式的值转换为命令行，并调用它。

---

::: header
Next: [Auto-loading sequences](Auto_002dloading-sequences.html#Auto_002dloading-sequences)]
:::
