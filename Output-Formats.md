---
tip: translate by openai@2023-06-24 00:50:40
...
---
description: Output Formats (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Output Formats (Debugging with GDB)
lang: en
resource-type: document
title: Output Formats (Debugging with GDB)
---
::: header
Next: [Memory](Memory.html#Memory)]
:::

---

### 10.5 Output Formats


By default, [GDB] prints a value according to its data type. Sometimes this is not what you want. For example, you might want to print a number in hex, or a pointer in decimal. Or you might want to view data in memory at a certain address as a character string or as an instruction. To do these things, specify an *output format* when you print a value.

> 默认情况下，GDB根据其数据类型打印一个值。有时这不是你想要的。例如，您可能希望以十六进制打印一个数字，或以十进制打印一个指针。或者，您可能希望以字符串或指令的形式查看某个地址处的内存中的数据。要做到这些，请在打印值时指定一个*输出格式*。


The simplest use of output formats is to say how to print a value already computed. This is done by starting the arguments of the `print` command with a slash and a format letter. The format letters supported are:

> 最简单的输出格式用法是说明如何打印已经计算出的值。这是通过在 `print` 命令的参数开头添加斜杠和格式字母来完成的。支持的格式字母为：

`x`

:   Print the binary representation of the value in hexadecimal.

`d`

:   Print the binary representation of the value in decimal.

`u`


:   Print the binary representation of the value as an decimal, as if it were unsigned.

> 打印出该值的二进制表示形式，就像它是无符号的十进制数一样。

`o`

:   Print the binary representation of the value in octal.

`t`


:   Print the binary representation of the value in binary. The letter '`t`

> 打印出二进制表示的值。字母't'

`a`

:

```
Print as an address, both absolute in hexadecimal and as an offset from the nearest preceding symbol. You can use this format used to discover where (in what function) an unknown address is located:

::: smallexample
``` smallexample
(gdb) p/a 0x54320
$3 = 0x54320 <_initialize_vx+396>
```

:::

The command `info symbol 0x54320` yields similar results. See [info symbol](Symbols.html#Symbols).

```

`c`


:   Cast the value to an integer (unlike other formats, this does not just reinterpret the underlying bits) and print it as a character constant. This prints both the numerical value and its character representation. The character representation is replaced with the octal escape '`\nnn` range.

> 将值转换为整数（与其他格式不同，这不仅仅是重新解释底层位）并将其打印为字符常量。这会打印数值和其字符表示形式。字符表示形式被替换为八进制转义'\nnn'范围。

```

Without this format, [GDB] displays `char`, `unsigned char`, and `signed char` data as character constants. Single-byte members of vectors are displayed as integer data.

```

`f`


:   Regard the bits of the value as a floating point number and print using typical floating point syntax.

> 将值的位看作浮点数，并使用典型的浮点数语法打印。

`s`

:   

```

Regard as a string, if possible. With this format, pointers to single-byte data are displayed as null-terminated strings and arrays of single-byte data are displayed as fixed-length strings. Other values are displayed in their natural types.

Without this format, [GDB] displays pointers to and arrays of `char`, `unsigned char`, and `signed char` as strings. Single-byte members of a vector are displayed as an integer array.

```

`z`


:   Like '`x`' formatting, the value is treated as an integer and printed as hexadecimal, but leading zeros are printed to pad the value to the size of the integer type.

> 就像'x'格式一样，值会被当作整数，并以十六进制的形式打印出来，但会在前面补零来使值符合整数类型的大小。

`r`

:   

```

Print using the '`raw`' format bypasses any Python pretty-printer which might exist.

```


For example, to print the program counter in hex (see [Registers](Registers.html#Registers)), type

> 例如，要以十六进制打印程序计数器（请参见[寄存器](Registers.html#Registers)），请输入

::: smallexample

```bash
p/x $pc
```

:::


Note that no space is required before the slash; this is because command names in [GDB] cannot contain a slash.

> 注意，在斜杠前不需要空格；这是因为[GDB]中的命令名称不能包含斜杠。


To reprint the last value in the value history with a different format, you can use the `print` command with just a format and no expression. For example, '`p/x`' reprints the last value in hex.

> 重新以不同格式打印出值历史中的最后一个值，可以使用只有格式而没有表达式的`print`命令。例如，'`p/x`' 将以十六进制重新打印最后一个值。

::: footnote

---

#### Footnotes

### [(11)](#DOCF11)

'`b`' stands for "byte"; see [Examining Memory](Memory.html#Memory).
:::

---

::: header
Next: [Memory](Memory.html#Memory)]
:::
