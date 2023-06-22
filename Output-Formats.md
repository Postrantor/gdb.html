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

The simplest use of output formats is to say how to print a value already computed. This is done by starting the arguments of the `print` command with a slash and a format letter. The format letters supported are:

`x`

:   Print the binary representation of the value in hexadecimal.

`d`

:   Print the binary representation of the value in decimal.

`u`

:   Print the binary representation of the value as an decimal, as if it were unsigned.

`o`

:   Print the binary representation of the value in octal.

`t`

:   Print the binary representation of the value in binary. The letter '`t`

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

```

Without this format, [GDB] displays `char`, `unsigned char`, and `signed char` data as character constants. Single-byte members of vectors are displayed as integer data.

```

`f`

:   Regard the bits of the value as a floating point number and print using typical floating point syntax.

`s`

:   

```

Regard as a string, if possible. With this format, pointers to single-byte data are displayed as null-terminated strings and arrays of single-byte data are displayed as fixed-length strings. Other values are displayed in their natural types.

Without this format, [GDB] displays pointers to and arrays of `char`, `unsigned char`, and `signed char` as strings. Single-byte members of a vector are displayed as an integer array.

```

`z`

:   Like '`x`' formatting, the value is treated as an integer and printed as hexadecimal, but leading zeros are printed to pad the value to the size of the integer type.

`r`

:   

```

Print using the '`raw`' format bypasses any Python pretty-printer which might exist.

```

For example, to print the program counter in hex (see [Registers](Registers.html#Registers)), type

::: smallexample

```bash
p/x $pc
```

:::

Note that no space is required before the slash; this is because command names in [GDB] cannot contain a slash.

To reprint the last value in the value history with a different format, you can use the `print` command with just a format and no expression. For example, '`p/x`' reprints the last value in hex.

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
