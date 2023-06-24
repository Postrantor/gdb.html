---
tip: translate by openai@2023-06-24 10:43:53
...
---
description: Symbols (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Symbols (Debugging with GDB)
lang: en
resource-type: document
title: Symbols (Debugging with GDB)
---
::: header
Next: [Altering](Altering.html#Altering)]
:::

---

## 16 Examining the Symbol Table


The commands described in this chapter allow you to inquire about the symbols (names of variables, functions and types) defined in your program. This information is inherent in the text of your program and does not change as your program executes. [GDB] (see [Choosing Files](File-Options.html#File-Options)), or by one of the file-management commands (see [Commands to Specify Files](Files.html#Files)).

> 本章节中描述的命令允许您查询程序中定义的符号（变量、函数和类型的名称）。此信息固有于您的程序文本中，在程序执行过程中不会改变（参见[选择文件](File-Options.html#File-Options)，或者使用文件管理命令（参见[指定文件命令](Files.html#Files)））。


Occasionally, you may need to refer to symbols that contain unusual characters, which [GDB]' as a single symbol, enclose it in single quotes; for example,

> 偶尔，您可能需要引用包含不寻常字符的符号，将[GDB]作为单个符号，用单引号括起来；例如，'。

::: smallexample

```bash
p 'foo.c'::x
```

:::

looks up the value of `x` in the scope of the file `foo.c`.

`set case-sensitive on`

`set case-sensitive off`

`set case-sensitive auto`


Normally, when [GDB] looks up symbols, it matches their names with case sensitivity determined by the current source language. Occasionally, you may wish to control that. The command `set case-sensitive` lets you do that by specifying `on` for case-sensitive matches or `off` for case-insensitive ones. If you specify `auto`, case sensitivity is reset to the default suitable for the source language. The default is case-sensitive matches for all languages except for Fortran, for which the default is case-insensitive matches.

> 一般来说，当GDB查找符号时，它会根据当前源语言的大小写敏感度来匹配它们的名称。有时，您可能希望控制这一点。命令`set case-sensitive`可以让您通过指定`on`来进行大小写敏感的匹配，或者指定`off`来进行大小写不敏感的匹配。如果您指定`auto`，则大小写敏感度将重置为适用于源语言的默认值。默认情况下，除了Fortran之外，所有语言的匹配都是大小写敏感的，而Fortran的默认匹配是大小写不敏感的。

`show case-sensitive`


This command shows the current setting of case sensitivity for symbols lookups.

> 这个命令显示当前符号查找的大小写敏感设置。

`set print type methods`

`set print type methods on`

`set print type methods off`

Normally, when [GDB] to omit the methods.

`show print type methods`


This command shows the current setting of method display when printing classes.

> 这个命令显示了打印类时当前的方法显示设置。

`set print type nested-type-limit limit`

`set print type nested-type-limit unlimited`


Set the limit of displayed nested types that the type printer will show. A `limit` of `unlimited` or `-1` will show all nested definitions. By default, the type printer will not show any nested types defined in classes.

> 设置类型打印机显示的嵌套类型的限制。`无限`或`-1`的`限制`将显示所有嵌套定义。默认情况下，类型打印机不会显示类中定义的任何嵌套类型。

`show print type nested-type-limit`


This command shows the current display limit of nested types when printing classes.

> 这个命令显示当打印类时嵌套类型的当前显示限制。

`set print type typedefs`

`set print type typedefs on`

`set print type typedefs off`


Normally, when [GDB] to omit the typedef definitions. Note that this controls whether the typedef definition itself is printed, not whether typedef names are substituted when printing other types.

> 一般来说，当使用GDB时会省略类型定义。请注意，这控制的是是否打印类型定义本身，而不是在打印其他类型时是否替换类型定义名称。

`show print type typedefs`


This command shows the current setting of typedef display when printing classes.

> 这个命令显示了打印类时typedef显示的当前设置。

`set print type hex`

`set print type hex on`

`set print type hex off`


When [GDB] prints sizes and offsets of struct members, it can use either the decimal or hexadecimal notation. You can select one or the other either by passing the appropriate flag to `ptype`, or by using the `set print type hex` command.

> 当[GDB]打印结构成员的大小和偏移量时，它可以使用十进制或十六进制的表示法。您可以通过传递适当的标志给`ptype`来选择其中一个，或者使用`set print type hex`命令。

`show print type hex`


This command shows whether the sizes and offsets of struct members are printed in decimal or hexadecimal notation.

> 这个命令显示结构体成员的大小和偏移量是以十进制还是十六进制表示法打印出来的。

`info address symbol`


Describe where the data for `symbol` is stored. For a register variable, this says which register it is kept in. For a non-register local variable, this prints the stack-frame offset at which the variable is always stored.

> 描述`symbol`的数据存储在哪里。对于寄存器变量，这表示它存储在哪个寄存器中。对于非寄存器局部变量，这会打印出变量总是存储在堆栈帧偏移量中的值。


Note the contrast with '`print &symbol`', which does not work at all for a register variable, and for a stack local variable prints the exact address of the current instantiation of the variable.

> 注意与'`print &symbol`'的对比，对于寄存器变量来说完全无效，而对于堆栈局部变量来说会打印出变量当前实例化的确切地址。

`info symbol addr`


Print the name of a symbol which is stored at the address `addr` prints the nearest symbol and an offset from it:

> 在地址`addr`存储的符号的名称打印出最近的符号及其偏移量：

::: smallexample

```bash
(gdb) info symbol 0x54320
_initialize_vx + 396 in section .text
```

:::


This is the opposite of the `info address` command. You can use it to find out the name of a variable or a function given its address.

> 这是`info address`命令的反向操作。您可以使用它根据地址查找变量或函数的名称。


For dynamically linked executables, the name of executable or shared library containing the symbol is also printed:

> 对于动态链接的可执行文件，也会打印出包含该符号的可执行文件或共享库的名称：

::: smallexample

```bash
(gdb) info symbol 0x400225
_start + 5 in section .text of /tmp/a.out
(gdb) info symbol 0x2aaaac2811cf
__read_nocancel + 6 in section .text of /usr/lib64/libc.so.6
```

:::

`demangle [-l language] [--] name`

Demangle `name` is demangled in the current language.

The '`--` begins with a dash.


The parameter `demangle-style` specifies how to interpret the kind of mangling used. See [Print Settings](Print-Settings.html#Print-Settings).

> 参数`demangle-style`指定如何解释使用的类型的编码。详见[打印设置](Print-Settings.html#Print-Settings)。

`whatis[/flags] [arg]`


Print the data type of `arg`, which can be either an expression or a name of a data type. With no argument, print the data type of `$`, the last value in the value history.

> 打印`arg`的数据类型，它可以是一个表达式或数据类型的名称。如果没有参数，则打印`$`的数据类型，即值历史中的最后一个值。


If `arg` is an expression (see [Expressions](Expressions.html#Expressions)), it is not actually evaluated, and any side-effecting operations (such as assignments or function calls) inside it do not take place.

> 如果`arg`是一个表达式（参见[表达式](Expressions.html#Expressions)），它并不会被实际计算，其中的任何有副作用的操作（例如赋值或函数调用）都不会发生。


If `arg` is a variable or an expression, `whatis` prints its literal type as it is used in the source code. If the type was defined using a `typedef`, `whatis` will *not* print the data type underlying the `typedef`. If the type of the variable or the expression is a compound data type, such as `struct` or `class`, `whatis` never prints their fields or methods. It just prints the `struct`/`class` name (a.k.a. its *tag*). If you want to see the members of such a compound data type, use `ptype`.

> 如果`arg`是一个变量或表达式，`whatis`会打印出它在源代码中使用的原始类型。如果类型是使用`typedef`定义的，`whatis`*不会*打印底层的数据类型。如果变量或表达式的类型是复合数据类型，比如`struct`或`class`，`whatis`永远不会打印它们的字段或方法。它只会打印`struct`/`class`的名字（又称其标签）。如果你想查看这种复合数据类型的成员，请使用`ptype`。


If `arg`. However, if that underlying type is also a `typedef`, `whatis` will not unroll it.

> 如果`arg`是一个底层类型，`whatis`将不会展开它，但如果它也是一个`typedef`，`whatis`不会展开它。

For C code, the type names may also have the form '`class class-name`'.

`flags` can be used to modify how the type is displayed. Available flags are:

`r`


:   Display in "raw" form. Normally, [GDB] substitutes template parameters and typedefs defined in a class when printing the class' members. The `/r` flag disables this.

> 显示"原始"形式。通常情况下，[GDB]在打印类成员时会替换类中定义的模板参数和typedefs。 `/r`标志禁用此功能。

`m`

:   Do not print methods defined in the class.

`M`


:   Print methods defined in the class. This is the default, but the flag exists in case you change the default with `set print type methods`.

> 打印类中定义的方法。这是默认值，但是如果你使用`set print type methods`更改了默认值，则存在标志。

`t`


:   Do not print typedefs defined in the class. Note that this controls whether the typedef definition itself is printed, not whether typedef names are substituted when printing other types.

> 不要打印类中定义的typedef。注意，这控制了打印typedef定义本身，而不是打印其他类型时是否替换typedef名称。

`T`


:   Print typedefs defined in the class. This is the default, but the flag exists in case you change the default with `set print type typedefs`.

> 打印类中定义的类型定义。这是默认值，但是可以通过`set print type typedefs`更改默认值。

`o`


:   Print the offsets and sizes of fields in a struct, similar to what the `pahole` tool does. This option implies the `/tm` flags.

> 打印结构体中字段的偏移量和大小，类似于`pahole`工具所做的。此选项包含`/tm`标志。

`x`


:   Use hexadecimal notation when printing offsets and sizes of fields in a struct.

> 使用十六进制标记打印结构体中的偏移量和字段大小。

`d`


:   Use decimal notation when printing offsets and sizes of fields in a struct.

> 使用十进制表示法打印结构体中的偏移量和字段大小。

```
For example, given the following declarations:

::: smallexample
``` smallexample
struct tuv
{
  int a1;
  char *a2;
  int a3;
};

struct xyz
{
  int f1;
  char f2;
  void *f3;
  struct tuv f4;
};

union qwe
{
  struct tuv fff1;
  struct xyz fff2;
};

struct tyu
{
  int a1 : 1;
  int a2 : 3;
  int a3 : 23;
  char a4 : 2;
  int64_t a5;
  int a6 : 5;
  int64_t a7 : 3;
};
```

:::

Issuing a [ptype /o struct tuv] command would print:

::: smallexample

```bash
(gdb) ptype /o struct tuv
/* offset      |    size */  type = struct tuv {
/*      0      |       4 */    int a1;
/* XXX  4-byte hole      */
/*      8      |       8 */    char *a2;
/*     16      |       4 */    int a3;

                               /* total size (bytes):   24 */
                             }
```

:::

Notice the format of the first column of comments. There, you can find two parts separated by the '`|`' character: the *offset*, which indicates where the field is located inside the struct, in bytes, and the *size* of the field. Another interesting line is the marker of a *hole* in the struct, indicating that it may be possible to pack the struct and make it use less space by reorganizing its fields.

It is also possible to print offsets inside an union:

::: smallexample

```bash
(gdb) ptype /o union qwe
/* offset      |    size */  type = union qwe {
/*                    24 */    struct tuv {
/*      0      |       4 */        int a1;
/* XXX  4-byte hole      */
/*      8      |       8 */        char *a2;
/*     16      |       4 */        int a3;

                                   /* total size (bytes):   24 */
                               } fff1;
/*                    40 */    struct xyz {
/*      0      |       4 */        int f1;
/*      4      |       1 */        char f2;
/* XXX  3-byte hole      */
/*      8      |       8 */        void *f3;
/*     16      |      24 */        struct tuv {
/*     16      |       4 */            int a1;
/* XXX  4-byte hole      */
/*     24      |       8 */            char *a2;
/*     32      |       4 */            int a3;

                                       /* total size (bytes):   24 */
                                   } f4;

                                   /* total size (bytes):   40 */
                               } fff2;

                               /* total size (bytes):   40 */
                             }
```

:::

In this case, since `struct tuv` and `struct xyz` occupy the same space (because we are dealing with an union), the offset is not printed for them. However, you can still examine the offset of each of these structures' fields.

Another useful scenario is printing the offsets of a struct containing bitfields:

::: smallexample

```bash
(gdb) ptype /o struct tyu
/* offset      |    size */  type = struct tyu {
/*      0:31   |       4 */    int a1 : 1;
/*      0:28   |       4 */    int a2 : 3;
/*      0: 5   |       4 */    int a3 : 23;
/*      3: 3   |       1 */    signed char a4 : 2;
/* XXX  3-bit hole       */
/* XXX  4-byte hole      */
/*      8      |       8 */    int64_t a5;
/*     16: 0   |       4 */    int a6 : 5;
/*     16: 5   |       8 */    int64_t a7 : 3;
/* XXX  7-byte padding   */

                               /* total size (bytes):   24 */
                             }
```

:::

Note how the offset information is now extended to also include the first bit of the bitfield.

```



`ptype[/flags] [arg]`

`ptype` accepts the same arguments as `whatis`, but prints a detailed description of the type, instead of just the name of the type. See [Expressions](Expressions.html#Expressions).


Contrary to `whatis`, `ptype` always unrolls any `typedef` s in its argument declaration, whether the argument is a variable, expression, or a data type. This means that `ptype` of a variable or an expression will not print literally its type as present in the source code---use `whatis` for that. `typedef` s at the pointer or reference targets are also unrolled. Only `typedef` s of fields, methods and inner `class typedef` s of `struct` s, `class` es and `union` s are not unrolled even with `ptype`.

> 相反，`ptype`总是展开其声明中的任何`typedef`，无论参数是变量、表达式还是数据类型。这意味着变量或表达式的`ptype`不会像源代码中那样直接打印它的类型---使用`whatis`来做这件事。指针或引用目标的`typedef`也会被展开。`struct`，`class`和`union`的字段、方法和内部`class typedef`的`typedef`即使使用`ptype`也不会被展开。

For example, for this variable declaration:

::: smallexample

```bash
typedef double real_t;
struct complex ;
typedef struct complex complex_t;
complex_t var;
real_t *real_pointer_var;
```

:::

the two commands give this output:

::: smallexample

```bash
(gdb) whatis var
type = complex_t
(gdb) ptype var
type = struct complex {
    real_t real;
    double imag;
}
(gdb) whatis complex_t
type = struct complex
(gdb) whatis struct complex
type = struct complex
(gdb) ptype struct complex
type = struct complex {
    real_t real;
    double imag;
}
(gdb) whatis real_pointer_var
type = real_t *
(gdb) ptype real_pointer_var
type = double *
```

:::


As with `whatis`, using `ptype` without an argument refers to the type of `$`, the last value in the value history.

> 就像`whatis`一样，使用`ptype`没有参数指的是`$`的类型，即值历史中的最后一个值。


Sometimes, programs use opaque data types or incomplete specifications of complex data structure. If the debug information included in the program does not allow [GDB]'. For example, given these declarations:

> 有时，程序使用不透明的数据类型或复杂数据结构的不完整规范。如果程序中包含的调试信息不允许[GDB]，例如，给定这些声明：

::: smallexample

```bash
    struct foo;
    struct foo *fooptr;
```

:::

but no definition for `struct foo` itself, [GDB] will say:

::: smallexample

```bash
  (gdb) ptype foo
  $1 = <incomplete type>
```

:::


"Incomplete type" is C terminology for data types that are not completely specified.

> "Incomplete type" 是 C 語言中用來指尚未完全定義的資料型態。


Othertimes, information about a variable's type is completely absent from the debug information included in the program. This most often happens when the program or library where the variable is defined includes no debug information at all. [GDB] has no type information shows:

> 有时，变量类型的信息完全没有包含在程序中的调试信息中。这通常发生在定义变量的程序或库中没有任何调试信息的情况下。[GDB]没有类型信息。

::: smallexample

```bash
  (gdb) ptype var
  type = <data variable, no debug info>
```

:::


See [no debug info variables](Variables.html#Variables), for how to print the values of such variables.

> 查看[无调试信息变量](Variables.html#Variables)，了解如何打印这些变量的值。

`info types [-q] [regexp]`


Print a brief description of all types whose names match the regular expression `regexp`' gives information only on types whose complete name is `value`.

> 打印所有名称与正则表达式`regexp`匹配的类型的简要描述，只提供完整名称为`value`的类型的信息。


In programs using different languages, [GDB]' (see [Set Language Automatically](Automatically.html#Automatically)) means to use the language of the type, other values mean to use the manually specified language (see [Set Language Manually](Manually.html#Manually)).

> 在使用不同语言的程序中，[GDB]（参见[自动设置语言]（Automatically.html#Automatically））意味着使用类型的语言，其他值意味着使用手动指定的语言（参见[手动设置语言]（Manually.html#Manually））。


This command differs from `ptype` in two ways: first, like `whatis`, it does not print a detailed description; second, it lists all source files and line numbers where a type is defined.

> 这条命令与`ptype`有两点不同：首先，像`whatis`一样，它不会打印详细的描述；其次，它会列出所有定义类型的源文件和行号。


The output from '`into types`', disables printing this header information.

> `使用"输出到类型"功能，禁止打印此头信息。`

`info type-printers`


Versions of [GDB] that ship with Python scripting enabled may have "type printers" available. When using `ptype` or `whatis`, these printers are consulted when the name of a type is needed. See [Type Printing API](Type-Printing-API.html#Type-Printing-API), for more information on writing type printers.

> 搭載Python腳本的GDB版本可能有“型別印表機”可用。當使用`ptype`或`whatis`時，這些印表機會在需要類型名稱時被查詢。有關編寫型別印表機的更多信息，請參閱[型別印表機API](Type-Printing-API.html#Type-Printing-API)。

`info type-printers` displays all the available type printers.

`enable type-printer name…`

`disable type-printer name…`

These commands can be used to enable or disable type printers.

`info scope locspec`


List all the variables local to the lexical scope of the code location that results from resolving `locspec`. For example:

> 列出所有局部变量，这些变量属于从解析`locspec`得出的代码位置的词法范围。例如：

::: smallexample

```bash
(gdb) info scope command_line_handler
Scope for command_line_handler:
Symbol rl is an argument at stack/frame offset 8, length 4.
Symbol linebuffer is in static storage at address 0x150a18, length 4.
Symbol linelength is in static storage at address 0x150a1c, length 4.
Symbol p is a local variable in register $esi, length 4.
Symbol p1 is a local variable in register $ebx, length 4.
Symbol nline is a local variable in register $edx, length 4.
Symbol repeat is a local variable at frame offset -8, length 4.
```

:::


This command is especially useful for determining what data to collect during a *trace experiment*, see [collect](Tracepoint-Actions.html#Tracepoint-Actions).

> 这个命令特别有用，可以用来确定在*跟踪实验*中应该收集什么数据，参见[collect](Tracepoint-Actions.html#Tracepoint-Actions)。

`info source`


Show information about the current source file---that is, the source file for the function containing the current point of execution:

> 显示有关当前源文件的信息---即包含当前执行点的函数的源文件

- the name of the source file, and the directory containing it,
- the directory it was compiled in,
- its length, in lines,
- which programming language it is written in,

- if the debug information provides it, the program that compiled the file (which may include, e.g., the compiler version and command line arguments),

> 如果调试信息提供，编译该文件的程序（可能包括，例如，编译器版本和命令行参数）

- whether the executable includes debugging information for that file, and if so, what format the information is in (e.g., STABS, Dwarf 2, etc.), and

> - 此可执行文件是否包含该文件的调试信息，如果有，信息的格式是什么（例如，STABS，Dwarf 2 等）？
- whether the debugging information includes information about preprocessor macros.

`info sources [-dirname | -basename] [--] [regexp]`


With no options '`info sources`. For each object file all of the associated source files are listed.

> 没有选项'`info sources`。列出所有与每个对象文件相关的源文件。


Each source file will only be printed once for each object file, but a single source file can be repeated in the output if it is part of multiple object files.

> 每个源文件对于每个对象文件只会被打印一次，但是如果一个源文件属于多个对象文件，它在输出中可能会被重复打印。

If the optional `regexp`').

By default, the `regexp` are shown.


It is possible that an object file may be printed in the list with no associated source files. This can happen when either no source files match `regexp` is unable to find any source file names.

> 可能会出现一个对象文件在列表中没有相关源文件的情况。这种情况可能是因为`regexp`无法找到任何源文件名。

`info functions [-q] [-n]`


Print the names and data types of all defined functions. Similarly to '`info types`', this command groups its output by source files and annotates each function definition with its source line number.

> 打印所有已定义函数的名称和数据类型。与 'info types' 类似，此命令按源文件对其输出进行分组，并用源文件行号注释每个函数定义。


In programs using different languages, [GDB]' (see [Set Language Automatically](Automatically.html#Automatically)) means to use the language of the function, other values mean to use the manually specified language (see [Set Language Manually](Manually.html#Manually)).

> 在使用不同语言的程序中，[GDB]（参见[自动设置语言]（Automatically.html#Automatically））意味着使用函数的语言，其他值意味着使用手动指定的语言（参见[手动设置语言]（Manually.html#Manually））。


The '`-n`' flag excludes *non-debugging symbols* from the results. A non-debugging symbol is a symbol that comes from the executable's symbol table, not from the debug information (for example, DWARF) associated with the executable.

> `-n` 标志会排除结果中的*非调试符号*。非调试符号是指来自可执行文件符号表的符号，而不是与可执行文件相关联的调试信息（例如DWARF）。


The optional flag '`-q`', disables printing header information and messages explaining why no functions have been printed.

> 可选标志'-q'禁用打印标头信息和解释为什么没有打印函数的消息。

`info functions [-q] [-n] [-t type_regexp] [regexp]`


Like '`info functions`', but only print the names and data types of the functions selected with the provided regexp(s).

> 像'`info functions`'一樣，但只列印出使用提供的正則表達式所選擇函數的名稱和資料類型。

If `regexp`'), they may be quoted with a backslash.


If `type_regexp`' finds the functions whose names start with `step` and that return int.

> 如果`type_regexp`找到以`step`开头且返回int的函数。

If both `regexp`.

`info variables [-q] [-n]`


Print the names and data types of all variables that are defined outside of functions (i.e. excluding local variables). The printed variables are grouped by source files and annotated with their respective source line numbers.

> 打印所有定义在函数外（不包括局部变量）的变量的名称和数据类型。打印的变量按源文件分组，并注明相应的源文件行号。


In programs using different languages, [GDB]' (see [Set Language Automatically](Automatically.html#Automatically)) means to use the language of the variable, other values mean to use the manually specified language (see [Set Language Manually](Manually.html#Manually)).

> 在使用不同语言的程序中，[GDB]（参见[自动设置语言]（Automatically.html#Automatically））意味着使用变量的语言，其他值意味着使用手动指定的语言（参见[手动设置语言]（Manually.html#Manually））。

The '`-n`' flag excludes non-debugging symbols from the results.


The optional flag '`-q`', disables printing header information and messages explaining why no variables have been printed.

> 可选标志 '-q' 禁用打印头信息和解释为什么没有变量被打印的消息。

`info variables [-q] [-n] [-t type_regexp] [regexp]`


Like [info variables], but only print the variables selected with the provided regexp(s).

> 就像[信息变量]一样，但只打印使用提供的正则表达式选择的变量。

If `regexp`.


If `type_regexp` contains space(s), it should be enclosed in quote characters. If needed, use backslash to escape the meaning of special characters or quotes.

> 如果`type_regexp`包含空格，应该用引号括起来。如果需要，可以使用反斜杠来转义特殊字符或引号的含义。

If both `regexp`.

`info modules [-q] [regexp]`


List all Fortran modules in the program, or all modules matching the optional regular expression `regexp`.

> 列出程序中的所有Fortran模块，或者所有与可选正则表达式'regexp'匹配的模块。


The optional flag '`-q`', disables printing header information and messages explaining why no modules have been printed.

> 可选标志'-q'禁用打印头信息和解释为什么没有打印模块的消息。

`info module functions [-q] [-m module-regexp] [-t type-regexp] [regexp]`

`info module variables [-q] [-m module-regexp] [-t type-regexp] [regexp]`


List all functions or variables within all Fortran modules. The set of functions or variables listed can be limited by providing some or all of the optional regular expressions. If `module-regexp` will be listed.

> 列出所有Fortran模块中的所有函数或变量。可以通过提供一些或所有可选正则表达式来限制列出的函数或变量集合。如果将列出`module-regexp`。


The optional flag '`-q`', disables printing header information and messages explaining why no functions or variables have been printed.

> 可选标志'-q'禁用打印头信息和解释为什么没有打印函数或变量的消息。

`info main`


Print the name of the starting function of the program. This serves primarily Fortran programs, which have a user-supplied name for the main subroutine.

> 打印程序的起始函数的名称。这主要针对Fortran程序，它们有一个用户提供的主子程序的名称。

`info classes`

`info classes regexp`


Display all Objective-C classes in your program, or (with the `regexp` argument) all those matching a particular regular expression.

> 显示程序中的所有Objective-C类，或者（使用`regexp`参数）显示所有匹配特定正则表达式的类。

`info selectors`

`info selectors regexp`


Display all Objective-C selectors in your program, or (with the `regexp` argument) all those matching a particular regular expression.

> 在程序中显示所有Objective-C选择器，或者（使用`regexp`参数）显示所有符合特定正则表达式的选择器。

`set opaque-type-resolution on`


Tell [GDB] to resolve opaque types. An opaque type is a type declared as a pointer to a `struct`, `class`, or `union`---for example, `struct MyType *`---that is used in one source file although the full declaration of `struct MyType` is in another source file. The default is on.

> 告诉GDB解析不透明类型。不透明类型是一种作为指向结构体、类或联合体的指针而声明的类型，例如`struct MyType *`，它在一个源文件中使用，而`struct MyType`的完整声明在另一个源文件中。默认情况下是打开的。


A change in the setting of this subcommand will not take effect until the next time symbols for a file are loaded.

> 这个子命令的设置更改不会在文件符号加载之前生效。

`set opaque-type-resolution off`


Tell [GDB] not to resolve opaque types. In this case, the type is printed as follows:

> 告诉GDB不要解析不透明的类型。在这种情况下，类型会按如下方式打印：

::: smallexample

```bash

```

:::

`show opaque-type-resolution`

Show whether opaque types are resolved or not.

`set print symbol-loading`

`set print symbol-loading full`

`set print symbol-loading brief`

`set print symbol-loading off`


The `set print symbol-loading` command allows you to control the printing of messages when [GDB] loads a collection of shared libraries at once it will only print one message regardless of the number of shared libraries. When set to `off` no messages are printed.

> 命令`set print symbol-loading`允许您控制[GDB]一次加载多个共享库时打印消息的情况，它只会打印一条消息，而不管共享库的数量。设置为`off`时不会打印任何消息。

`show print symbol-loading`


Show whether messages will be printed when a [GDB] command entered from the keyboard causes symbol information to be loaded.

> 请显示当从键盘输入[GDB]命令加载符号信息时，是否会打印消息。

`maint print symbols [-pc address] [filename]`

`maint print symbols [-objfile objfile] [-source source] [--] [filename]`

`maint print psymbols [-objfile objfile] [-pc address] [--] [filename]`

`maint print psymbols [-objfile objfile] [-source source] [--] [filename]`

`maint print msymbols [-objfile objfile] [--] [filename]`


Write a dump of debugging symbol data into the file `filename` may be a symbol like `main`. If `-source source` is specified, only dump symbols for that source file.

> 将调试符号数据写入文件`filename`可能是一个符号，比如`main`。如果指定了`-source source`，只转储该源文件的符号。


These commands are used to debug the [GDB]' just dumps "minimal symbols", e.g., "ELF symbols".

> 这些命令用于调试GDB，只转储“最小符号”，例如“ELF符号”。


See [Commands to Specify Files](Files.html#Files), for a discussion of how [GDB] reads symbols (in the description of `symbol-file`).

> 请参阅[指定文件的命令](Files.html#Files)，了解[GDB]如何读取符号（在`symbol-file`的描述中）。

`maint info symtabs [ regexp ]`

`maint info psymtabs [ regexp ]`


List the `struct symtab` or `struct partial_symtab` structures whose names match `regexp` debugging this one to examine a particular structure in more detail. For example:

> 列出名称与`regexp`匹配的`struct symtab`或`struct partial_symtab`结构，调试这个以更详细地检查特定结构。例如：

::: smallexample

```bash
(gdb) maint info psymtabs dwarf2read
{ objfile /home/gnu/build/gdb/gdb
  ((struct objfile *) 0x82e69d0)
  { psymtab /home/gnu/src/gdb/dwarf2read.c
    ((struct partial_symtab *) 0x8474b10)
    readin no
    fullname (null)
    text addresses 0x814d3c8 -- 0x8158074
    globals (* (struct partial_symbol **) 0x8507a08 @ 9)
    statics (* (struct partial_symbol **) 0x40e95b78 @ 2882)
    dependencies (none)
  }
}
(gdb) maint info symtabs
(gdb)
```

:::


We see that there is one partial symbol table whose filename contains the string '`dwarf2read` to read the symtab for the compilation unit containing that function:

> 我们看到有一个部分符号表，它的文件名包含字符串“dwarf2read”，用于读取包含该函数的编译单元的符号表：

::: smallexample

```bash
(gdb) break dwarf2_psymtab_to_symtab
Breakpoint 1 at 0x814e5da: file /home/gnu/src/gdb/dwarf2read.c,
line 1574.
(gdb) maint info symtabs
{ objfile /home/gnu/build/gdb/gdb
  ((struct objfile *) 0x82e69d0)
  { symtab /home/gnu/src/gdb/dwarf2read.c
    ((struct symtab *) 0x86c1f38)
    dirname (null)
    fullname (null)
    blockvector ((struct blockvector *) 0x86c1bd0) (primary)
    linetable ((struct linetable *) 0x8370fa0)
    debugformat DWARF 2
  }
}
(gdb)
```

:::

`maint info line-table [ regexp ]`


List the `struct linetable` from all `struct symtab` instances whose name matches `regexp` is not given, list the `struct linetable` from all `struct symtab`. For example:

> 列出所有符合正则表达式的`struct symtab`实例的`struct linetable`，如果没有给出，则列出所有`struct symtab`的`struct linetable`。例如：

::: smallexample

```bash
(gdb) maint info line-table
objfile: /home/gnu/build/a.out ((struct objfile *) 0x6120000e0d40)
compunit_symtab: simple.cpp ((struct compunit_symtab *) 0x6210000ff450)
symtab: /home/gnu/src/simple.cpp ((struct symtab *) 0x6210000ff4d0)
linetable: ((struct linetable *) 0x62100012b760):
INDEX  LINE   ADDRESS            IS-STMT PROLOGUE-END
0      3      0x0000000000401110 Y
1      4      0x0000000000401114 Y       Y
2      9      0x0000000000401120 Y
3      10     0x0000000000401124 Y       Y
4      10     0x0000000000401129
5      15     0x0000000000401130 Y
6      16     0x0000000000401134 Y       Y
7      16     0x0000000000401139
8      21     0x0000000000401140 Y
9      22     0x000000000040114f Y       Y
10     22     0x0000000000401154
11     END    0x000000000040115a Y
```

:::


The '`IS-STMT`' column indicates that a given address is an adequate place to set a breakpoint at the first instruction following a function prologue.

> `IS-STMT` 列表明给定地址是一个适当的地方，在函数序言之后的第一条指令处设置断点。

`set always-read-ctf [on|off]`

`show always-read-ctf`


When off, CTF debug info is only read if DWARF debug info is not present. When on, CTF debug info is read regardless of whether DWARF debug info is present. The default value is off.

> 当关闭时，如果没有DWARF调试信息，则只读取CTF调试信息。当打开时，无论是否存在DWARF调试信息，都会读取CTF调试信息。默认值是关闭的。

`maint set symbol-cache-size size`


Set the size of the symbol cache to `size`. The default size is intended to be good enough for debugging most applications. This option exists to allow for experimenting with different sizes.

> 设置符号缓存的大小为“size”。默认大小足以调试大多数应用程序。此选项的存在是为了允许尝试不同的大小。

`maint show symbol-cache-size`

Show the size of the symbol cache.

`maint print symbol-cache`


Print the contents of the symbol cache. This is useful when debugging symbol cache issues.

> 打印符号缓存的内容。当调试符号缓存问题时，这很有用。

`maint print symbol-cache-statistics`


Print symbol cache usage statistics. This helps determine how well the cache is being utilized.

> 打印符号缓存使用统计信息。这有助于确定缓存的使用效果如何。

`maint flush symbol-cache`

`maint flush-symbol-cache`


Flush the contents of the symbol cache, all entries are removed. This command is useful when debugging the symbol cache. It is also useful when collecting performance data. The command `maint flush-symbol-cache` is deprecated in favor of `maint flush symbol-cache`..

> 清空符号缓存的内容，所有条目都将被移除。此命令在调试符号缓存时非常有用。在收集性能数据时也很有用。命令'maint flush-symbol-cache'已被弃用，改用'maint flush symbol-cache'。

`maint set ignore-prologue-end-flag [on|off]`


Enable or disable the use of the '`PROLOGUE-END` ignores the flag and relies on prologue analyzers to skip function prologues.

> 启用或禁用'PROLOGUE-END'标志，并依靠序言分析器跳过函数序言。

`maint show ignore-prologue-end-flag`

Show whether [GDB]' flag.

---

::: header
Next: [Altering](Altering.html#Altering)]
:::
