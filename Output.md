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

`echo text`

Print `text`'.

A backslash at the end of `text` can be used, as in C, to continue the command onto subsequent lines. For example,

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

`output/fmt expression`

Print the value of `expression`. You can use the same formats as for `print`. See [Output Formats](Output-Formats.html#Output-Formats), for more information.

`printf template, expressions…`

Print the values of one or more `expressions`, exactly as a C program would do by executing the code below:

::: smallexample

```bash
printf (template, expressions…);
```

:::

As in `C` `printf`, ordinary characters in `template` to be evaluated, their values converted and formatted according to type and style information encoded in the conversion specifications, and then printed.

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
- The type modifiers '`hh`' are not supported.
- The conversion letter '`n`') is not supported.
- The conversion letters '`a`' are not supported.

Note that the '`ll`' type modifier is supported only if `long double` type is available.

As in `C`, `printf` supports simple backslash-escape sequences, such as `\n`, '`\t`', that consist of backslash followed by a single character. Octal and hexadecimal escape sequences are not supported.

Additionally, `printf` supports conversion specifications for DFP (*Decimal Floating Point*) types using the following length modifiers together with a floating point specifier. letters:

- '`H`' for printing `Decimal32` types.
- '`D`' for printing `Decimal64` types.
- '`DD`' for printing `Decimal128` types.

If the underlying `C` implementation used to build [GDB] to use.

In case there is no such `C` support, no additional modifiers will be available and the value will be printed in the standard way.

Here's an example of printing DFP types using the above conversion letters:

::: smallexample

```bash
printf "D32: %Hf - D64: %Df - D128: %DDf\n",1.2345df,1.2E10dd,1.2E1dl
```

:::

Additionally, `printf` supports a special '`%V` command (see [Examining Data](Data.html#Data)):

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

::: smallexample

```bash
(gdb) printf "Array is: %V[Hello]\n", array
Array is: [Hello]
```

:::

`eval template, expressions…`

Convert the values of one or more `expressions` to a command line, and call it.

---

::: header
Next: [Auto-loading sequences](Auto_002dloading-sequences.html#Auto_002dloading-sequences)]
:::
