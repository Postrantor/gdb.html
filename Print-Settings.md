---
tip: translate by openai@2023-06-24 01:11:49
...
---
description: Print Settings (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Print Settings (Debugging with GDB)
lang: en
resource-type: document
title: Print Settings (Debugging with GDB)
---
::: header
Next: [Pretty Printing](Pretty-Printing.html#Pretty-Printing)]
:::

---

### 10.9 Print Settings


[GDB] provides the following ways to control how arrays, structures, and symbols are printed.

> [GDB] 提供以下方式来控制数组、结构和符号的打印方式。

These settings are useful for debugging programs in any language:

`set print address`

`set print address on`


[GDB] prints memory addresses showing the location of stack traces, structure values, pointer values, breakpoints, and so forth, even when it also displays the contents of those addresses. The default is `on`. For example, this is what a stack frame display looks like with `set print address on`:

> [GDB]会打印出内存地址，显示堆栈跟踪，结构值，指针值，断点等的位置，即使它也显示了这些地址的内容。默认是开启的。例如，使用“set print address on”可以得到如下的堆栈帧显示：

::: smallexample

```bash
(gdb) f
#0  set_quotes (lq=0x34c78 "<<", rq=0x34c88 ">>")
    at input.c:530
530         if (lquote != def_lquote)
```

:::

`set print address off`


Do not print addresses when displaying their contents. For example, this is the same stack frame displayed with `set print address off`:

> 不要在显示内容时打印地址。例如，这是使用“set print address off”显示的相同堆栈帧：

::: smallexample

```bash
(gdb) set print addr off
(gdb) f
#0  set_quotes (lq="<<", rq=">>") at input.c:530
530         if (lquote != def_lquote)
```

:::


You can use '`set print address off` interface. For example, with `print address off`, you should get the same text for backtraces on all machines---whether or not they involve pointer arguments.

> 你可以使用`set print address off`接口。例如，使用`print address off`，无论是否涉及指针参数，你应该在所有机器上得到相同的回溯文本。

`show print address`

Show whether or not addresses are to be printed.


When [GDB] to print the source file and line number when it prints a symbolic address:

> 当[GDB]打印出一个符号地址时，打印源文件和行号。

`set print symbol-filename on`

:

```
Tell [GDB] to print the source file name and line number of a symbol in the symbolic form of an address.
```

`set print symbol-filename off`


:   Do not print source file name and line number of a symbol. This is the default.

> 不打印符号的源文件名称和行号。这是默认设置。

`show print symbol-filename`


:   Show whether or not [GDB] will print the source file name and line number of a symbol in the symbolic form of an address.

> 请帮助我翻译：显示[GDB]是否会在符号地址的符号形式中打印源文件名称和行号。


Another situation where it is helpful to show symbol filenames and line numbers is when disassembling code; [GDB] shows you the line number and source file that corresponds to each instruction.

> 在反汇编代码时，显示符号文件名和行号也很有帮助；[GDB]会显示每条指令对应的行号和源文件。


Also, you may wish to see the symbolic form only if the address being printed is reasonably close to the closest earlier symbol:

> 如果打印的地址与最近的符号相当接近，你可能希望只看象征形式。

`set print max-symbolic-offset max-offset`
`set print max-symbolic-offset unlimited`

:

```
Tell [GDB] to always print the symbolic form of an address if any symbol precedes it. Zero is equivalent to `unlimited`.
```

`show print max-symbolic-offset`


:   Ask how large the maximum offset is that [GDB] prints in a symbolic address.

> 问GDB在符号地址中打印的最大偏移量有多大？


If you have a pointer and you are not sure where it points, try '`set print symbol-filename on`:

> 如果你有一个指针，你不确定它指向哪里，试试“设置打印符号文件名”:

::: smallexample

```bash
(gdb) set print symbol-filename on
(gdb) p/a ptt
$4 = 0xe008 <t in hi2.c>
```

:::

> *Warning:* For pointers that point to a local variable, '`p/a`' does not show the symbol name and filename of the referent, even with the appropriate `set print` options turned on.

You can also enable '`/a`':

`set print symbol on`


:   Tell [GDB] to print the symbol corresponding to an address, if one exists.

> 告诉GDB打印对应地址的符号，如果存在的话。

`set print symbol off`


:   Tell [GDB] will still print the symbol corresponding to pointers to functions. This is the default.

> 告诉GDB它仍然会打印指向函数的指针对应的符号。这是默认的。

`show print symbol`


:   Show whether [GDB] will display the symbol corresponding to an address.

> 检查GDB是否会显示与地址对应的符号。

Other settings control how different kinds of objects are printed:

`set print array`

`set print array on`


Pretty print arrays. This format is more convenient to read, but uses more space. The default is off.

> 格式化打印数组。这种格式更容易阅读，但需要更多的空间。默认是关闭的。

`set print array off`

Return to compressed format for arrays.

`show print array`


Show whether compressed or pretty format is selected for displaying arrays.

> 显示是否为数组选择了压缩或者漂亮的格式。

`set print array-indexes`

`set print array-indexes on`


Print the index of each element when displaying arrays. May be more convenient to locate a given element in the array or quickly find the index of a given element in that printed array. The default is off.

> 当显示数组时，打印每个元素的索引。可能更方便地定位数组中的给定元素或快速找到打印数组中给定元素的索引。默认情况下是关闭的。

`set print array-indexes off`

Stop printing element indexes when displaying arrays.

`show print array-indexes`

Show whether the index of each element is printed when displaying arrays.

`set print nibbles`

`set print nibbles on`


Print binary values in groups of four bits, known as *nibbles*, when using the print command of [GDB]'. For example, this is what it looks like with `set print nibbles on`:

> 使用GDB的打印命令，以四位二进制值（被称为nibbles）的组合打印。例如，使用`set print nibbles on`时，看起来像这样：

::: smallexample

```bash
(gdb) print val_flags
$1 = 1230
(gdb) print/t val_flags
$2 = 0100 1100 1110
```

:::

`set print nibbles off`

Don't printing binary values in groups. This is the default.

`show print nibbles`

Show whether to print binary values in groups of four bits.

`set print characters number-of-characters`

`set print characters elements`

`set print characters unlimited`


Set a limit on how many characters of a string [GDB] starts, this limit is set to `elements`.

> 设定一个字符串[GDB]的开始字符数的限制，这个限制设定为“元素”。

`show print characters`

Display the number of characters of a large string that [GDB] will print.

`set print elements number-of-elements`

`set print elements unlimited`


Set a limit on how many elements of an array [GDB] to `unlimited` or zero means that the number of elements to print is unlimited.

> 设置一个限制，将数组[GDB]中的元素数量设置为`无限`或者零，意味着要打印的元素数量是无限的。


When printing very large arrays, whose size is greater than `max-value-size` (see [max-value-size](Value-Sizes.html#set-max_002dvalue_002dsize)), if the `print elements` is set such that the size of the elements being printed is less than or equal to `max-value-size`, then [GDB] will print the array (up to the `print elements` limit), and only `max-value-size` worth of data will be added into the value history (see [Value History](Value-History.html#Value-History)).

> 当打印非常大的数组，其大小大于`max-value-size`（参见[max-value-size](Value-Sizes.html#set-max_002dvalue_002dsize)），如果设置`print elements`使得打印的元素的大小小于或等于`max-value-size`，那么[GDB]将会打印数组（最多打印`print elements`限制），而只有`max-value-size`的数据会被添加到值历史记录中（参见[Value History](Value-History.html#Value-History)）。

`show print elements`

Display the number of elements of a large array that [GDB] will print.

`set print frame-arguments value`


This command allows to control how the values of arguments are printed when the debugger prints a frame (see [Frames](Frames.html#Frames)). The possible values are:

> 这个命令允许控制调试器打印帧时参数值的打印方式（参见[帧](Frames.html#Frames)）。可能的值有：

`all`

:   The values of all arguments are printed.

`scalars`


:   Print the value of an argument only if it is a scalar. The value of more complex arguments such as arrays, structures, unions, etc, is replaced by `…`. This is the default. Here is an example where only scalar arguments are shown:

> 只有参数是标量时才打印参数的值。数组、结构、联合等更复杂的参数的值会被替换为“…”，这是默认的。下面是一个只显示标量参数的示例：

```
::: smallexample
``` smallexample
#1  0x08048361 in call_me (i=3, s=…, ss=0xbf8d508c, u=…, e=green)
  at frame-args.c:23
```

:::

```

`none`


:   None of the argument values are printed. Instead, the value of each argument is replaced by `…`. In this case, the example above now becomes:

> 没有打印任何参数值。相反，每个参数的值都被“…”替换。在这种情况下，上面的示例现在变成：

```

::: smallexample

```bash
#1  0x08048361 in call_me (i=…, s=…, ss=…, u=…, e=…)
  at frame-args.c:23
```

:::

```

`presence`


:   Only the presence of arguments is indicated by `…`. The `…` are not printed for function without any arguments. None of the argument names and values are printed. In this case, the example above now becomes:

> 只有参数的存在才会用 `...` 来表示，没有参数的函数不会打印 `...`，也不会打印参数的名称和值。在这种情况下，上面的例子就变成：

```

::: smallexample

```bash
#1  0x08048361 in call_me (…) at frame-args.c:23
```

:::

```


By default, only scalar arguments are printed. This command can be used to configure the debugger to print the value of all arguments, regardless of their type. However, it is often advantageous to not print the value of more complex parameters. For instance, it reduces the amount of information printed in each frame, making the backtrace more readable. Also, it improves performance when displaying Ada frames, because the computation of large arguments can sometimes be CPU-intensive, especially in large applications. Setting `print frame-arguments` to `scalars` (the default), `none` or `presence` avoids this computation, thus speeding up the display of each Ada frame.

> 默认情况下，只有标量参数会被打印出来。此命令可以用来配置调试器打印所有参数的值，无论它们的类型如何。然而，不打印更复杂参数的值往往是有益的。例如，它减少了每个帧中打印的信息量，使回溯更加可读。此外，它还提高了在显示 Ada 帧时的性能，因为计算大参数有时可能是 CPU 密集型的，特别是在大型应用程序中。将 `print frame-arguments` 设置为 `scalars`（默认值）、`none` 或 `presence` 可以避免此计算，从而加快每个 Ada 帧的显示速度。

`show print frame-arguments`


Show how the value of arguments should be displayed when printing a frame.

> 请示意如何在打印框架时显示参数的值。



`set print raw-frame-arguments on`

Print frame arguments in raw, non pretty-printed, form.

`set print raw-frame-arguments off`


Print frame arguments in pretty-printed form, if there is a pretty-printer for the value (see [Pretty Printing](Pretty-Printing.html#Pretty-Printing)), otherwise print the value in raw form. This is the default.

> 如果值有可用的美化打印器（参见[Pretty Printing](Pretty-Printing.html#Pretty-Printing)），则以美化格式打印帧参数，否则以原始格式打印值。这是默认行为。

`show print raw-frame-arguments`

Show whether to print frame arguments in raw form.



`set print entry-values value`




Set printing of frame argument values at function entry. In some cases [GDB] can determine the value of function argument which was passed by the function caller, even if the value was modified inside the called function and therefore is different. With optimized code, the current value could be unavailable, but the entry value may still be known.

> 在函数入口处设置帧参数值的打印。在某些情况下，[GDB]可以确定被调用函数调用者传递的函数参数的值，即使该值在被调用函数内被修改，并因此不同。对于优化的代码，当前值可能不可用，但入口值仍可能已知。


The default value is `default` (see below for its description). Older [GDB] behaved as with the setting `no`. Compilers not supporting this feature will behave in the `default` setting the same way as with the `no` setting.

> 默认值为'default'（见下面的描述）。较早的GDB行为与设置'no'一致。不支持此功能的编译器将以'default'设置与'no'设置行为相同。


This functionality is currently supported only by DWARF 2 debugging format and the compiler has to produce '`DW_TAG_call_site` during compilation, to get this information.

> 这个功能目前只支持DWARF 2调试格式，编译器必须在编译期间产生'DW_TAG_call_site'才能获得这些信息。

The `value` parameter can be one of the following:

`no`


:   Print only actual parameter values, never print values from function entry point.

> 只打印实际参数值，永远不要打印从函数入口点获得的值。

```

::: smallexample

```bash
#0  equal (val=5)
#0  different (val=6)
#0  lost (val=<optimized out>)
#0  born (val=10)
#0  invalid (val=<optimized out>)
```

:::

```

`only`


:   Print only parameter values from function entry point. The actual parameter values are never printed.

> 只从函数入口点打印参数值。实际参数值永不打印。

```

::: smallexample

```bash
#0  equal (val@entry=5)
#0  different (val@entry=5)
#0  lost (val@entry=5)
#0  born (val@entry=<optimized out>)
#0  invalid (val@entry=<optimized out>)
```

:::

```

`preferred`


:   Print only parameter values from function entry point. If value from function entry point is not known while the actual value is known, print the actual value for such parameter.

> 仅从函数入口点打印参数值。如果在实际值已知的情况下函数入口点的值未知，则为此类参数打印实际值。

```

::: smallexample

```bash
#0  equal (val@entry=5)
#0  different (val@entry=5)
#0  lost (val@entry=5)
#0  born (val=10)
#0  invalid (val@entry=<optimized out>)
```

:::

```

`if-needed`


:   Print actual parameter values. If actual parameter value is not known while value from function entry point is known, print the entry point value for such parameter.

> 打印实际参数值。如果在函数入口点知道实际参数值未知的情况下，则为此类参数打印入口点值。

```

::: smallexample

```bash
#0  equal (val=5)
#0  different (val=6)
#0  lost (val@entry=5)
#0  born (val=10)
#0  invalid (val=<optimized out>)
```

:::

```

`both`


:   Always print both the actual parameter value and its value from function entry point, even if values of one or both are not available due to compiler optimizations.

> 总是打印实际参数值及其从函数入口点获得的值，即使由于编译器优化而导致其中一个或两个值不可用。

```

::: smallexample

```bash
#0  equal (val=5, val@entry=5)
#0  different (val=6, val@entry=5)
#0  lost (val=<optimized out>, val@entry=5)
#0  born (val=10, val@entry=<optimized out>)
#0  invalid (val=<optimized out>, val@entry=<optimized out>)
```

:::

```

`compact`


:   Print the actual parameter value if it is known and also its value from function entry point if it is known. If neither is known, print for the actual value `<optimized out>`. If not in MI mode (see [GDB/MI](GDB_002fMI.html#GDB_002fMI)) and if both values are known and identical, print the shortened `param=param@entry=VALUE` notation.

> 如果已知实际参数值，则打印实际参数值，并且如果已知函数入口点的值，也打印它的值。如果两者都不知道，则打印实际值<优化掉>。如果不在MI模式下（参见[GDB/MI](GDB_002fMI.html#GDB_002fMI)），并且如果两个值都已知且相同，则打印缩写的`param=param@entry=VALUE`形式。

```

::: smallexample

```bash
#0  equal (val=val@entry=5)
#0  different (val=6, val@entry=5)
#0  lost (val@entry=5)
#0  born (val=10)
#0  invalid (val=<optimized out>)
```

:::

```

`default`


:   Always print the actual parameter value. Print also its value from function entry point, but only if it is known. If not in MI mode (see [GDB/MI](GDB_002fMI.html#GDB_002fMI)) and if both values are known and identical, print the shortened `param=param@entry=VALUE` notation.

> 总是打印实际参数值。如果已知，也打印函数入口点的值。如果不是在MI模式下（参见[GDB/MI]（GDB_002fMI.html#GDB_002fMI）），并且如果两个值都已知且相同，则打印缩写的`param = param@entry = VALUE`表示法。

```

::: smallexample

```bash
#0  equal (val=val@entry=5)
#0  different (val=6, val@entry=5)
#0  lost (val=<optimized out>, val@entry=5)
#0  born (val=10)
#0  invalid (val=<optimized out>)
```

:::

```


For analysis messages on possible failures of frame argument values at function entry resolution see [set debug entry-values](Tail-Call-Frames.html#set-debug-entry_002dvalues).

> 为了分析框架参数值在函数入口解析可能出现的失败信息，请参阅[设置debug entry-values](Tail-Call-Frames.html#set-debug-entry_002dvalues)。

`show print entry-values`


Show the method being used for printing of frame argument values at function entry.

> 顯示在函數進入時打印框架參數值的方法。



`set print frame-info value`




This command allows to control the information printed when the debugger prints a frame. See [Frames](Frames.html#Frames), [Backtrace](Backtrace.html#Backtrace), for a general explanation about frames and frame information. Note that some other settings (such as `set print frame-arguments` and `set print address`) are also influencing if and how some frame information is displayed. In particular, the frame program counter is never printed if `set print address` is off.

> 这个命令允许控制调试器打印帧时所打印的信息。有关帧和帧信息的一般解释，请参见[帧](Frames.html#Frames)和[回溯](Backtrace.html#Backtrace)。请注意，一些其他设置（例如`set print frame-arguments`和`set print address`）也会影响某些帧信息是否以及如何显示。特别是，如果`set print address`关闭，则永远不会打印帧程序计数器。

The possible values for `set print frame-info` are:

`short-location`


:   Print the frame level, the program counter (if not at the beginning of the location source line), the function, the function arguments.

> 打印帧级别、程序计数器（如果不在源代码行的开头）、函数以及函数参数。

`location`


:   Same as `short-location` but also print the source file and source line number.

> 和`short-location`一样，但也会打印源文件和源行号。

`location-and-address`


:   Same as `location` but print the program counter even if located at the beginning of the location source line.

> 相同于`位置`，但即使位于位置源行的开头，也会打印程序计数器。

`source-line`


:   Print the program counter (if not at the beginning of the location source line), the line number and the source line.

> 打印程序计数器（如果不在源代码行的开头）、行号和源代码行。

`source-and-location`

:   Print what `location` and `source-line` are printing.

`auto`


:   The information printed for a frame is decided automatically by the [GDB] command that prints a frame. For example, `frame` prints the information printed by `source-and-location` while `stepi` will switch between `source-line` and `source-and-location` depending on the program counter. The default value is `auto`.

> GDB 命令决定了每一帧的打印信息。例如，`frame` 命令会打印 `source-and-location` 的信息，而 `stepi` 命令会根据程序计数器的不同而切换 `source-line` 和 `source-and-location` 两种模式。默认值是 `auto`。



`set print repeats number-of-repeats`

`set print repeats unlimited`




Set the threshold for suppressing display of repeated array elements. When the number of consecutive identical elements of an array exceeds the threshold, [GDB] is the number of identical repetitions, instead of displaying the identical elements themselves. Setting the threshold to `unlimited` or zero will cause all elements to be individually printed. The default threshold is 10.

> 设置阈值以抑制显示重复的数组元素。当数组的连续相同元素的数量超过阈值时，[GDB] 是相同重复的数量，而不是显示相同的元素本身。将阈值设置为`unlimited`或零会导致所有元素都单独打印。默认阈值为10。

`show print repeats`

Display the current threshold for printing repeated identical elements.



`set print max-depth depth`

`set print max-depth unlimited`




Set the threshold after which nested structures are replaced with ellipsis, this can make visualising deeply nested structures easier.

> 设定阈值，超过该阈值时，嵌套结构将被替换为省略号，这可以使深层嵌套结构的可视化更加容易。

For example, given this C code

::: smallexample

```bash
typedef struct s1  s1;
typedef struct s2  s2;
typedef struct s3  s3;
typedef struct s4  s4;

s4 var = ;
```

:::

The following table shows how different values of `depth`:

`depth`'

---

unlimited                    `$1 = `
`0`                          `$1 = `
`1`                          `$1 = `
`2`                          `$1 = `
`3`                          `$1 = `
`4`                          `$1 = `


To see the contents of structures that have been hidden the user can either increase the print max-depth, or they can print the elements of the structure that are visible, for example

> 用户可以增加打印最大深度来查看已隐藏结构的内容，或者他们可以打印可见结构的元素，例如。

::: smallexample

```bash
(gdb) set print max-depth 2
(gdb) p var
$1 = 
(gdb) p var.d
$2 = 
(gdb) p var.d.c
$3 = 
```

:::


The pattern used to replace nested structures varies based on language, for most languages `` is used, but Fortran uses `(...)`.

> 不同的语言使用不同的模式来替换嵌套结构，大多数语言使用``，但Fortran使用`(...)`。

`show print max-depth`


Display the current threshold after which nested structures are replaces with ellipsis.

> 显示当前嵌套结构被省略号替换的阈值。

`set print memory-tag-violations`

`set print memory-tag-violations on`


Cause [GDB] to display additional information about memory tag violations when printing pointers and addresses.

> 因为[GDB]在打印指针和地址时，可以显示有关内存标签违规的附加信息。

`set print memory-tag-violations off`

Stop printing memory tag violation information.

`show print memory-tag-violations`


Show whether memory tag violation information is displayed when printing pointers and addresses.

> 显示在打印指针和地址时是否显示内存标记违规信息。

`set print null-stop`


Cause [GDB] is encountered. This is useful when large arrays actually contain only short strings. The default is off.

> 由于遇到GDB，这在大数组实际上只包含短字符串时很有用。默认情况下是关闭的。

`show print null-stop`

Show whether [GDB] character.

`set print pretty on`


Cause [GDB] to print structures in an indented format with one member per line, like this:

> 因为GDB可以以缩进格式打印结构，每行一个成员，就像这样：

::: smallexample

```bash
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

`set print pretty off`

Cause [GDB] to print structures in a compact format, like this:

::: smallexample

```bash
$1 = , \
meat = 0x54 "Pork"}
```

:::

This is the default format.

`show print pretty`

Show which format [GDB] is using to print structures.

`set print raw-values on`


Print values in raw form, without applying the pretty printers for the value.

> 打印原始值，不使用格式化程序。

`set print raw-values off`


Print values in pretty-printed form, if there is a pretty-printer for the value (see [Pretty Printing](Pretty-Printing.html#Pretty-Printing)), otherwise print the value in raw form.

> 如果值有可以进行漂亮打印的打印机（参见[漂亮打印](Pretty-Printing.html#Pretty-Printing))，则以漂亮的格式打印值，否则以原始格式打印值。

The default setting is "off".

`show print raw-values`

Show whether to print values in raw form.

`set print sevenbit-strings on`


Print using only seven-bit characters; if this option is set, [GDB]) and you use the high-order bit of characters as a marker or "meta" bit.

> 使用七位字符打印；如果设置了此选项，[GDB]）并使用字符的高位作为标记或“元”位。

`set print sevenbit-strings off`


Print full eight-bit characters. This allows the use of more international character sets, and is the default.

> 打印全八位字符。这允许使用更多的国际字符集，并且是默认的。

`show print sevenbit-strings`

Show whether or not [GDB] is printing only seven-bit characters.

`set print union on`


Tell [GDB] to print unions which are contained in structures and other unions. This is the default setting.

> 告诉GDB打印包含在结构体和其他联合体中的联合体，这是默认设置。

`set print union off`

Tell [GDB]"` instead.

`show print union`


Ask [GDB] whether or not it will print unions which are contained in structures and other unions.

> 询问GDB是否会打印包含在结构中和其他联合体中的联合体。

For example, given the declarations

::: smallexample

```bash
typedef enum  Species;
typedef enum  Tree_forms;
typedef enum 
              Bug_forms;

struct thing {
  Species it;
  union {
    Tree_forms tree;
    Bug_forms bug;
  } form;
};

struct thing foo = ;
```

:::

with `set print union on` in effect '`p foo`' would print

::: smallexample

```bash
$1 = 
```

:::

and with `set print union off` in effect it would print

::: smallexample

```bash
$1 = 
```

:::

`set print union` affects programs written in C-like languages and in Pascal.

These settings are of interest when debugging C++ programs:

`set print demangle`

`set print demangle on`


Print C++ names in their source form rather than in the encoded ("mangled") form passed to the assembler and linker for type-safe linkage. The default is on.

> 打印C++名称以源代码形式而不是经过编码（“混淆”）形式传递给汇编器和链接器进行类型安全链接。默认情况下是开启的。

`show print demangle`

Show whether C++ names are printed in mangled or demangled form.

`set print asm-demangle`

`set print asm-demangle on`


Print C++ names in their source form rather than their mangled form, even in assembler code printouts such as instruction disassemblies. The default is off.

> 在汇编代码的输出（如指令反汇编）中，打印C++名称以其原始形式而不是混淆形式。默认情况下是关闭的。

`show print asm-demangle`


Show whether C++ names in assembly listings are printed in mangled or demangled form.

> 检查汇编列表中C++的名称是以经过编码（mangled）还是解码（demangled）的形式打印出来。

`set demangle-style style`


Choose among several encoding schemes used by different compilers to represent C++ names. If you omit `style` choose a decoding style by inspecting your program.

> 在不同的编译器中使用的几种编码方案中选择一种用于表示C++名称。如果省略`样式`，请通过检查程序选择解码样式。

`show demangle-style`

Display the encoding style currently in use for decoding C++ symbols.

`set print object`

`set print object on`


When displaying a pointer to an object, identify the *actual* (derived) type of the object rather than the *declared* type, using the virtual function table. Note that the virtual function table is required---this feature can only work for objects that have run-time type identification; a single virtual method in the object's declared type is sufficient. Note that this setting is also taken into account when working with variable objects via MI (see [GDB/MI](GDB_002fMI.html#GDB_002fMI)).

> 当显示指向对象的指针时，使用虚拟函数表识别对象的实际（派生）类型，而不是声明的类型。请注意，虚拟函数表是必需的---此功能仅适用于具有运行时类型识别的对象；对象声明类型中的单个虚拟方法就足够了。请注意，在通过MI使用变量对象时也会考虑此设置（参见[GDB / MI]（GDB_002fMI.html#GDB_002fMI））。

`set print object off`


Display only the declared type of objects, without reference to the virtual function table. This is the default setting.

> 只显示声明的对象类型，而不涉及虚函数表。这是默认设置。

`show print object`

Show whether actual, or declared, object types are displayed.

`set print static-members`

`set print static-members on`

Print static members when displaying a C++ object. The default is on.

`set print static-members off`

Do not print static members when displaying a C++ object.

`show print static-members`

Show whether C++ static members are printed or not.

`set print pascal_static-members`

`set print pascal_static-members on`

Print static members when displaying a Pascal object. The default is on.

`set print pascal_static-members off`

Do not print static members when displaying a Pascal object.

`show print pascal_static-members`

Show whether Pascal static members are printed or not.

`set print vtbl`

`set print vtbl on`


Pretty print C++ virtual function tables. The default is off. (The `vtbl` commands do not work on programs compiled with the HP ANSI C++ compiler (`aCC`).)

> 在使用HP ANSI C++编译器（aCC）编译的程序中，不能用vtbl命令来格式化输出C++虚函数表（默认情况下是关闭的）。

`set print vtbl off`

Do not pretty print C++ virtual function tables.

`show print vtbl`

Show whether C++ virtual function tables are pretty printed, or not.

---

::: header
Next: [Pretty Printing](Pretty-Printing.html#Pretty-Printing)]
:::
