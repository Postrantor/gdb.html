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

Occasionally, you may need to refer to symbols that contain unusual characters, which [GDB]' as a single symbol, enclose it in single quotes; for example,

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

`show case-sensitive`

This command shows the current setting of case sensitivity for symbols lookups.

`set print type methods`

`set print type methods on`

`set print type methods off`

Normally, when [GDB] to omit the methods.

`show print type methods`

This command shows the current setting of method display when printing classes.

`set print type nested-type-limit limit`

`set print type nested-type-limit unlimited`

Set the limit of displayed nested types that the type printer will show. A `limit` of `unlimited` or `-1` will show all nested definitions. By default, the type printer will not show any nested types defined in classes.

`show print type nested-type-limit`

This command shows the current display limit of nested types when printing classes.

`set print type typedefs`

`set print type typedefs on`

`set print type typedefs off`

Normally, when [GDB] to omit the typedef definitions. Note that this controls whether the typedef definition itself is printed, not whether typedef names are substituted when printing other types.

`show print type typedefs`

This command shows the current setting of typedef display when printing classes.

`set print type hex`

`set print type hex on`

`set print type hex off`

When [GDB] prints sizes and offsets of struct members, it can use either the decimal or hexadecimal notation. You can select one or the other either by passing the appropriate flag to `ptype`, or by using the `set print type hex` command.

`show print type hex`

This command shows whether the sizes and offsets of struct members are printed in decimal or hexadecimal notation.

`info address symbol`

Describe where the data for `symbol` is stored. For a register variable, this says which register it is kept in. For a non-register local variable, this prints the stack-frame offset at which the variable is always stored.

Note the contrast with '`print &symbol`', which does not work at all for a register variable, and for a stack local variable prints the exact address of the current instantiation of the variable.

`info symbol addr`

Print the name of a symbol which is stored at the address `addr` prints the nearest symbol and an offset from it:

::: smallexample

```bash
(gdb) info symbol 0x54320
_initialize_vx + 396 in section .text
```

:::

This is the opposite of the `info address` command. You can use it to find out the name of a variable or a function given its address.

For dynamically linked executables, the name of executable or shared library containing the symbol is also printed:

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

`whatis[/flags] [arg]`

Print the data type of `arg`, which can be either an expression or a name of a data type. With no argument, print the data type of `$`, the last value in the value history.

If `arg` is an expression (see [Expressions](Expressions.html#Expressions)), it is not actually evaluated, and any side-effecting operations (such as assignments or function calls) inside it do not take place.

If `arg` is a variable or an expression, `whatis` prints its literal type as it is used in the source code. If the type was defined using a `typedef`, `whatis` will *not* print the data type underlying the `typedef`. If the type of the variable or the expression is a compound data type, such as `struct` or `class`, `whatis` never prints their fields or methods. It just prints the `struct`/`class` name (a.k.a. its *tag*). If you want to see the members of such a compound data type, use `ptype`.

If `arg`. However, if that underlying type is also a `typedef`, `whatis` will not unroll it.

For C code, the type names may also have the form '`class class-name`'.

`flags` can be used to modify how the type is displayed. Available flags are:

`r`

:   Display in "raw" form. Normally, [GDB] substitutes template parameters and typedefs defined in a class when printing the class' members. The `/r` flag disables this.

`m`

:   Do not print methods defined in the class.

`M`

:   Print methods defined in the class. This is the default, but the flag exists in case you change the default with `set print type methods`.

`t`

:   Do not print typedefs defined in the class. Note that this controls whether the typedef definition itself is printed, not whether typedef names are substituted when printing other types.

`T`

:   Print typedefs defined in the class. This is the default, but the flag exists in case you change the default with `set print type typedefs`.

`o`

:   Print the offsets and sizes of fields in a struct, similar to what the `pahole` tool does. This option implies the `/tm` flags.

`x`

:   Use hexadecimal notation when printing offsets and sizes of fields in a struct.

`d`

:   Use decimal notation when printing offsets and sizes of fields in a struct.

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

Sometimes, programs use opaque data types or incomplete specifications of complex data structure. If the debug information included in the program does not allow [GDB]'. For example, given these declarations:

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

Othertimes, information about a variable's type is completely absent from the debug information included in the program. This most often happens when the program or library where the variable is defined includes no debug information at all. [GDB] has no type information shows:

::: smallexample

```bash
  (gdb) ptype var
  type = <data variable, no debug info>
```

:::

See [no debug info variables](Variables.html#Variables), for how to print the values of such variables.

`info types [-q] [regexp]`

Print a brief description of all types whose names match the regular expression `regexp`' gives information only on types whose complete name is `value`.

In programs using different languages, [GDB]' (see [Set Language Automatically](Automatically.html#Automatically)) means to use the language of the type, other values mean to use the manually specified language (see [Set Language Manually](Manually.html#Manually)).

This command differs from `ptype` in two ways: first, like `whatis`, it does not print a detailed description; second, it lists all source files and line numbers where a type is defined.

The output from '`into types`', disables printing this header information.

`info type-printers`

Versions of [GDB] that ship with Python scripting enabled may have "type printers" available. When using `ptype` or `whatis`, these printers are consulted when the name of a type is needed. See [Type Printing API](Type-Printing-API.html#Type-Printing-API), for more information on writing type printers.

`info type-printers` displays all the available type printers.

`enable type-printer name…`

`disable type-printer name…`

These commands can be used to enable or disable type printers.

`info scope locspec`

List all the variables local to the lexical scope of the code location that results from resolving `locspec`. For example:

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

`info source`

Show information about the current source file---that is, the source file for the function containing the current point of execution:

- the name of the source file, and the directory containing it,
- the directory it was compiled in,
- its length, in lines,
- which programming language it is written in,
- if the debug information provides it, the program that compiled the file (which may include, e.g., the compiler version and command line arguments),
- whether the executable includes debugging information for that file, and if so, what format the information is in (e.g., STABS, Dwarf 2, etc.), and
- whether the debugging information includes information about preprocessor macros.

`info sources [-dirname | -basename] [--] [regexp]`

With no options '`info sources`. For each object file all of the associated source files are listed.

Each source file will only be printed once for each object file, but a single source file can be repeated in the output if it is part of multiple object files.

If the optional `regexp`').

By default, the `regexp` are shown.

It is possible that an object file may be printed in the list with no associated source files. This can happen when either no source files match `regexp` is unable to find any source file names.

`info functions [-q] [-n]`

Print the names and data types of all defined functions. Similarly to '`info types`', this command groups its output by source files and annotates each function definition with its source line number.

In programs using different languages, [GDB]' (see [Set Language Automatically](Automatically.html#Automatically)) means to use the language of the function, other values mean to use the manually specified language (see [Set Language Manually](Manually.html#Manually)).

The '`-n`' flag excludes *non-debugging symbols* from the results. A non-debugging symbol is a symbol that comes from the executable's symbol table, not from the debug information (for example, DWARF) associated with the executable.

The optional flag '`-q`', disables printing header information and messages explaining why no functions have been printed.

`info functions [-q] [-n] [-t type_regexp] [regexp]`

Like '`info functions`', but only print the names and data types of the functions selected with the provided regexp(s).

If `regexp`'), they may be quoted with a backslash.

If `type_regexp`' finds the functions whose names start with `step` and that return int.

If both `regexp`.

`info variables [-q] [-n]`

Print the names and data types of all variables that are defined outside of functions (i.e. excluding local variables). The printed variables are grouped by source files and annotated with their respective source line numbers.

In programs using different languages, [GDB]' (see [Set Language Automatically](Automatically.html#Automatically)) means to use the language of the variable, other values mean to use the manually specified language (see [Set Language Manually](Manually.html#Manually)).

The '`-n`' flag excludes non-debugging symbols from the results.

The optional flag '`-q`', disables printing header information and messages explaining why no variables have been printed.

`info variables [-q] [-n] [-t type_regexp] [regexp]`

Like [info variables], but only print the variables selected with the provided regexp(s).

If `regexp`.

If `type_regexp` contains space(s), it should be enclosed in quote characters. If needed, use backslash to escape the meaning of special characters or quotes.

If both `regexp`.

`info modules [-q] [regexp]`

List all Fortran modules in the program, or all modules matching the optional regular expression `regexp`.

The optional flag '`-q`', disables printing header information and messages explaining why no modules have been printed.

`info module functions [-q] [-m module-regexp] [-t type-regexp] [regexp]`

`info module variables [-q] [-m module-regexp] [-t type-regexp] [regexp]`

List all functions or variables within all Fortran modules. The set of functions or variables listed can be limited by providing some or all of the optional regular expressions. If `module-regexp` will be listed.

The optional flag '`-q`', disables printing header information and messages explaining why no functions or variables have been printed.

`info main`

Print the name of the starting function of the program. This serves primarily Fortran programs, which have a user-supplied name for the main subroutine.

`info classes`

`info classes regexp`

Display all Objective-C classes in your program, or (with the `regexp` argument) all those matching a particular regular expression.

`info selectors`

`info selectors regexp`

Display all Objective-C selectors in your program, or (with the `regexp` argument) all those matching a particular regular expression.

`set opaque-type-resolution on`

Tell [GDB] to resolve opaque types. An opaque type is a type declared as a pointer to a `struct`, `class`, or `union`---for example, `struct MyType *`---that is used in one source file although the full declaration of `struct MyType` is in another source file. The default is on.

A change in the setting of this subcommand will not take effect until the next time symbols for a file are loaded.

`set opaque-type-resolution off`

Tell [GDB] not to resolve opaque types. In this case, the type is printed as follows:

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

`show print symbol-loading`

Show whether messages will be printed when a [GDB] command entered from the keyboard causes symbol information to be loaded.

`maint print symbols [-pc address] [filename]`

`maint print symbols [-objfile objfile] [-source source] [--] [filename]`

`maint print psymbols [-objfile objfile] [-pc address] [--] [filename]`

`maint print psymbols [-objfile objfile] [-source source] [--] [filename]`

`maint print msymbols [-objfile objfile] [--] [filename]`

Write a dump of debugging symbol data into the file `filename` may be a symbol like `main`. If `-source source` is specified, only dump symbols for that source file.

These commands are used to debug the [GDB]' just dumps "minimal symbols", e.g., "ELF symbols".

See [Commands to Specify Files](Files.html#Files), for a discussion of how [GDB] reads symbols (in the description of `symbol-file`).

`maint info symtabs [ regexp ]`

`maint info psymtabs [ regexp ]`

List the `struct symtab` or `struct partial_symtab` structures whose names match `regexp` debugging this one to examine a particular structure in more detail. For example:

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

`set always-read-ctf [on|off]`

`show always-read-ctf`

When off, CTF debug info is only read if DWARF debug info is not present. When on, CTF debug info is read regardless of whether DWARF debug info is present. The default value is off.

`maint set symbol-cache-size size`

Set the size of the symbol cache to `size`. The default size is intended to be good enough for debugging most applications. This option exists to allow for experimenting with different sizes.

`maint show symbol-cache-size`

Show the size of the symbol cache.

`maint print symbol-cache`

Print the contents of the symbol cache. This is useful when debugging symbol cache issues.

`maint print symbol-cache-statistics`

Print symbol cache usage statistics. This helps determine how well the cache is being utilized.

`maint flush symbol-cache`

`maint flush-symbol-cache`

Flush the contents of the symbol cache, all entries are removed. This command is useful when debugging the symbol cache. It is also useful when collecting performance data. The command `maint flush-symbol-cache` is deprecated in favor of `maint flush symbol-cache`..

`maint set ignore-prologue-end-flag [on|off]`

Enable or disable the use of the '`PROLOGUE-END` ignores the flag and relies on prologue analyzers to skip function prologues.

`maint show ignore-prologue-end-flag`

Show whether [GDB]' flag.

---

::: header
Next: [Altering](Altering.html#Altering)]
:::
