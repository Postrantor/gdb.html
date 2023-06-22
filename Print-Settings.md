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

These settings are useful for debugging programs in any language:

`set print address`

`set print address on`

[GDB] prints memory addresses showing the location of stack traces, structure values, pointer values, breakpoints, and so forth, even when it also displays the contents of those addresses. The default is `on`. For example, this is what a stack frame display looks like with `set print address on`:

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

::: smallexample

```bash
(gdb) set print addr off
(gdb) f
#0  set_quotes (lq="<<", rq=">>") at input.c:530
530         if (lquote != def_lquote)
```

:::

You can use '`set print address off` interface. For example, with `print address off`, you should get the same text for backtraces on all machines---whether or not they involve pointer arguments.

`show print address`

Show whether or not addresses are to be printed.

When [GDB] to print the source file and line number when it prints a symbolic address:

`set print symbol-filename on`

:

```
Tell [GDB] to print the source file name and line number of a symbol in the symbolic form of an address.
```

`set print symbol-filename off`

:   Do not print source file name and line number of a symbol. This is the default.

`show print symbol-filename`

:   Show whether or not [GDB] will print the source file name and line number of a symbol in the symbolic form of an address.

Another situation where it is helpful to show symbol filenames and line numbers is when disassembling code; [GDB] shows you the line number and source file that corresponds to each instruction.

Also, you may wish to see the symbolic form only if the address being printed is reasonably close to the closest earlier symbol:

`set print max-symbolic-offset max-offset`
`set print max-symbolic-offset unlimited`

:

```
Tell [GDB] to always print the symbolic form of an address if any symbol precedes it. Zero is equivalent to `unlimited`.
```

`show print max-symbolic-offset`

:   Ask how large the maximum offset is that [GDB] prints in a symbolic address.

If you have a pointer and you are not sure where it points, try '`set print symbol-filename on`:

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

`set print symbol off`

:   Tell [GDB] will still print the symbol corresponding to pointers to functions. This is the default.

`show print symbol`

:   Show whether [GDB] will display the symbol corresponding to an address.

Other settings control how different kinds of objects are printed:

`set print array`

`set print array on`

Pretty print arrays. This format is more convenient to read, but uses more space. The default is off.

`set print array off`

Return to compressed format for arrays.

`show print array`

Show whether compressed or pretty format is selected for displaying arrays.

`set print array-indexes`

`set print array-indexes on`

Print the index of each element when displaying arrays. May be more convenient to locate a given element in the array or quickly find the index of a given element in that printed array. The default is off.

`set print array-indexes off`

Stop printing element indexes when displaying arrays.

`show print array-indexes`

Show whether the index of each element is printed when displaying arrays.

`set print nibbles`

`set print nibbles on`

Print binary values in groups of four bits, known as *nibbles*, when using the print command of [GDB]'. For example, this is what it looks like with `set print nibbles on`:

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

`show print characters`

Display the number of characters of a large string that [GDB] will print.

`set print elements number-of-elements`

`set print elements unlimited`

Set a limit on how many elements of an array [GDB] to `unlimited` or zero means that the number of elements to print is unlimited.

When printing very large arrays, whose size is greater than `max-value-size` (see [max-value-size](Value-Sizes.html#set-max_002dvalue_002dsize)), if the `print elements` is set such that the size of the elements being printed is less than or equal to `max-value-size`, then [GDB] will print the array (up to the `print elements` limit), and only `max-value-size` worth of data will be added into the value history (see [Value History](Value-History.html#Value-History)).

`show print elements`

Display the number of elements of a large array that [GDB] will print.

`set print frame-arguments value`

This command allows to control how the values of arguments are printed when the debugger prints a frame (see [Frames](Frames.html#Frames)). The possible values are:

`all`

:   The values of all arguments are printed.

`scalars`

:   Print the value of an argument only if it is a scalar. The value of more complex arguments such as arrays, structures, unions, etc, is replaced by `…`. This is the default. Here is an example where only scalar arguments are shown:

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

```

::: smallexample

```bash
#1  0x08048361 in call_me (…) at frame-args.c:23
```

:::

```

By default, only scalar arguments are printed. This command can be used to configure the debugger to print the value of all arguments, regardless of their type. However, it is often advantageous to not print the value of more complex parameters. For instance, it reduces the amount of information printed in each frame, making the backtrace more readable. Also, it improves performance when displaying Ada frames, because the computation of large arguments can sometimes be CPU-intensive, especially in large applications. Setting `print frame-arguments` to `scalars` (the default), `none` or `presence` avoids this computation, thus speeding up the display of each Ada frame.

`show print frame-arguments`

Show how the value of arguments should be displayed when printing a frame.



`set print raw-frame-arguments on`

Print frame arguments in raw, non pretty-printed, form.

`set print raw-frame-arguments off`

Print frame arguments in pretty-printed form, if there is a pretty-printer for the value (see [Pretty Printing](Pretty-Printing.html#Pretty-Printing)), otherwise print the value in raw form. This is the default.

`show print raw-frame-arguments`

Show whether to print frame arguments in raw form.



`set print entry-values value`



Set printing of frame argument values at function entry. In some cases [GDB] can determine the value of function argument which was passed by the function caller, even if the value was modified inside the called function and therefore is different. With optimized code, the current value could be unavailable, but the entry value may still be known.

The default value is `default` (see below for its description). Older [GDB] behaved as with the setting `no`. Compilers not supporting this feature will behave in the `default` setting the same way as with the `no` setting.

This functionality is currently supported only by DWARF 2 debugging format and the compiler has to produce '`DW_TAG_call_site` during compilation, to get this information.

The `value` parameter can be one of the following:

`no`

:   Print only actual parameter values, never print values from function entry point.

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

`show print entry-values`

Show the method being used for printing of frame argument values at function entry.



`set print frame-info value`



This command allows to control the information printed when the debugger prints a frame. See [Frames](Frames.html#Frames), [Backtrace](Backtrace.html#Backtrace), for a general explanation about frames and frame information. Note that some other settings (such as `set print frame-arguments` and `set print address`) are also influencing if and how some frame information is displayed. In particular, the frame program counter is never printed if `set print address` is off.

The possible values for `set print frame-info` are:

`short-location`

:   Print the frame level, the program counter (if not at the beginning of the location source line), the function, the function arguments.

`location`

:   Same as `short-location` but also print the source file and source line number.

`location-and-address`

:   Same as `location` but print the program counter even if located at the beginning of the location source line.

`source-line`

:   Print the program counter (if not at the beginning of the location source line), the line number and the source line.

`source-and-location`

:   Print what `location` and `source-line` are printing.

`auto`

:   The information printed for a frame is decided automatically by the [GDB] command that prints a frame. For example, `frame` prints the information printed by `source-and-location` while `stepi` will switch between `source-line` and `source-and-location` depending on the program counter. The default value is `auto`.



`set print repeats number-of-repeats`

`set print repeats unlimited`



Set the threshold for suppressing display of repeated array elements. When the number of consecutive identical elements of an array exceeds the threshold, [GDB] is the number of identical repetitions, instead of displaying the identical elements themselves. Setting the threshold to `unlimited` or zero will cause all elements to be individually printed. The default threshold is 10.

`show print repeats`

Display the current threshold for printing repeated identical elements.



`set print max-depth depth`

`set print max-depth unlimited`



Set the threshold after which nested structures are replaced with ellipsis, this can make visualising deeply nested structures easier.

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

`show print max-depth`

Display the current threshold after which nested structures are replaces with ellipsis.

`set print memory-tag-violations`

`set print memory-tag-violations on`

Cause [GDB] to display additional information about memory tag violations when printing pointers and addresses.

`set print memory-tag-violations off`

Stop printing memory tag violation information.

`show print memory-tag-violations`

Show whether memory tag violation information is displayed when printing pointers and addresses.

`set print null-stop`

Cause [GDB] is encountered. This is useful when large arrays actually contain only short strings. The default is off.

`show print null-stop`

Show whether [GDB] character.

`set print pretty on`

Cause [GDB] to print structures in an indented format with one member per line, like this:

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

`set print raw-values off`

Print values in pretty-printed form, if there is a pretty-printer for the value (see [Pretty Printing](Pretty-Printing.html#Pretty-Printing)), otherwise print the value in raw form.

The default setting is "off".

`show print raw-values`

Show whether to print values in raw form.

`set print sevenbit-strings on`

Print using only seven-bit characters; if this option is set, [GDB]) and you use the high-order bit of characters as a marker or "meta" bit.

`set print sevenbit-strings off`

Print full eight-bit characters. This allows the use of more international character sets, and is the default.

`show print sevenbit-strings`

Show whether or not [GDB] is printing only seven-bit characters.

`set print union on`

Tell [GDB] to print unions which are contained in structures and other unions. This is the default setting.

`set print union off`

Tell [GDB]"` instead.

`show print union`

Ask [GDB] whether or not it will print unions which are contained in structures and other unions.

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

`show print demangle`

Show whether C++ names are printed in mangled or demangled form.

`set print asm-demangle`

`set print asm-demangle on`

Print C++ names in their source form rather than their mangled form, even in assembler code printouts such as instruction disassemblies. The default is off.

`show print asm-demangle`

Show whether C++ names in assembly listings are printed in mangled or demangled form.

`set demangle-style style`

Choose among several encoding schemes used by different compilers to represent C++ names. If you omit `style` choose a decoding style by inspecting your program.

`show demangle-style`

Display the encoding style currently in use for decoding C++ symbols.

`set print object`

`set print object on`

When displaying a pointer to an object, identify the *actual* (derived) type of the object rather than the *declared* type, using the virtual function table. Note that the virtual function table is required---this feature can only work for objects that have run-time type identification; a single virtual method in the object's declared type is sufficient. Note that this setting is also taken into account when working with variable objects via MI (see [GDB/MI](GDB_002fMI.html#GDB_002fMI)).

`set print object off`

Display only the declared type of objects, without reference to the virtual function table. This is the default setting.

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

`set print vtbl off`

Do not pretty print C++ virtual function tables.

`show print vtbl`

Show whether C++ virtual function tables are pretty printed, or not.

---

::: header
Next: [Pretty Printing](Pretty-Printing.html#Pretty-Printing)]
:::
