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

`print [[options] --] expr`
`print [[options] --] /f expr`

:   `expr` is a letter specifying the format; see [Output Formats](Output-Formats.html#Output-Formats).

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

A more low-level way of examining data is with the `x` command. It examines data in memory at a specified address and prints it in a specified format. See [Examining Memory](Memory.html#Memory).

If you are interested in information about types, or about how the fields of a struct or a class are declared, use the `ptype expr` command rather than `print`. See [Examining the Symbol Table](Symbols.html#Symbols).



Another way of examining values of expressions and type information is through the Python extension command `explore` (available only if the [GDB] build is configured with `--with-python`). It offers an interactive way to start at the highest level (or, the most abstract level) of the data type of an expression (or, the data type itself) and explore all the way down to leaf scalar values/fields embedded in the higher level data types.

`explore arg`

:   `arg` is either an expression (in the source language), or a type visible in the current context of the program being debugged.

The working of the `explore` command can be illustrated with an example. If a data type `struct ComplexStruct` is defined in your C program as

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

Similar to exploring values, you can use the `explore` command to explore types. Instead of specifying a value (which is typically a variable name or an expression valid in the current context of the program being debugged), you specify a type name. If you consider the same example as above, your can explore the type `struct ComplexStruct` by passing the argument `struct ComplexStruct` to the `explore` command.

::: smallexample

```bash
(gdb) explore struct ComplexStruct
```

:::

By responding to the prompts appropriately in the subsequent interactive session, you can explore the type `struct ComplexStruct` in a manner similar to how the value `cs` was explored in the above example.

The `explore` command also has two sub-commands, `explore value` and `explore type`. The former sub-command is a way to explicitly specify that value exploration of the argument is being invoked, while the latter is a way to explicitly specify that type exploration of the argument is being invoked.

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
• [Ambiguous Expressions](Ambiguous-Expressions.html#Ambiguous-Expressions):        Ambiguous Expressions
• [Variables](Variables.html#Variables):                                            Program variables
• [Arrays](Arrays.html#Arrays):                                                     Artificial arrays
• [Output Formats](Output-Formats.html#Output-Formats):                             Output formats
• [Memory](Memory.html#Memory):                                                     Examining memory
• [Memory Tagging](Memory-Tagging.html#Memory-Tagging):                             Memory Tagging
• [Auto Display](Auto-Display.html#Auto-Display):                                   Automatic display
• [Print Settings](Print-Settings.html#Print-Settings):                             Print settings
• [Pretty Printing](Pretty-Printing.html#Pretty-Printing):                                         Python pretty printing
• [Value History](Value-History.html#Value-History):                                               Value history
• [Convenience Vars](Convenience-Vars.html#Convenience-Vars):                                      Convenience variables
• [Convenience Funs](Convenience-Funs.html#Convenience-Funs):                                      Convenience functions
• [Registers](Registers.html#Registers):                                                           Registers
• [Floating Point Hardware](Floating-Point-Hardware.html#Floating-Point-Hardware):                 Floating point hardware
• [Vector Unit](Vector-Unit.html#Vector-Unit):                                                     Vector Unit
• [OS Information](OS-Information.html#OS-Information):                                            Auxiliary data provided by operating system
• [Memory Region Attributes](Memory-Region-Attributes.html#Memory-Region-Attributes):              Memory region attributes
• [Dump/Restore Files](Dump_002fRestore-Files.html#Dump_002fRestore-Files):                        Copy between memory and a file
• [Core File Generation](Core-File-Generation.html#Core-File-Generation):                          Cause a program dump its core
• [Character Sets](Character-Sets.html#Character-Sets):                                            Debugging programs that use a different character set than GDB does
• [Caching Target Data](Caching-Target-Data.html#Caching-Target-Data):                             Data caching for targets
• [Searching Memory](Searching-Memory.html#Searching-Memory):                                      Searching memory for a sequence of bytes
• [Value Sizes](Value-Sizes.html#Value-Sizes):                                                     Managing memory allocated for values

---

---

::: header
Next: [Optimized Code](Optimized-Code.html#Optimized-Code)]
:::
