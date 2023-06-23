---
description: Variables (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Variables (Debugging with GDB)
lang: en
resource-type: document
title: Variables (Debugging with GDB)
---
::: header
Next: [Arrays](Arrays.html#Arrays)]
:::

---

### 10.3 Program Variables

The most common kind of expression to use is the name of a variable in your program.

Variables in expressions are understood in the selected stack frame (see [Selecting a Frame](Selection.html#Selection)); they must be either:

- global (or file-static)

or

- visible according to the scope rules of the programming language from the point of execution in that frame

This means that in the function

::: smallexample

```bash
foo (a)
     int a;
{
  bar (a);
  {
    int b = test ();
    bar (b);
  }
}
```

:::

you can examine and use the variable `a` whenever your program is executing within the function `foo`, but you can only use or examine the variable `b` while your program is executing inside the block where `b` is declared.

There is an exception: you can refer to a variable or function whose scope is a single source file even if the current execution point is not in this file. But it is possible to have more than one such variable or function with the same name (in different source files). If that happens, referring to that name has unpredictable effects. If you wish, you can specify a static variable in a particular function or file by using the colon-colon (`::`) notation:

::: smallexample

```bash
file::variable
function::variable
```

:::

Here `file`:

::: smallexample

```bash
(gdb) p 'f2.c'::x
```

:::

The `::` notation is normally used for referring to static variables, since you typically disambiguate uses of local variables in functions by selecting the appropriate frame and using the simple name of the variable. However, you may also use this notation to refer to local variables in frames enclosing the selected frame:

::: smallexample

```bash
void
foo (int a)
{
  if (a < 10)
    bar (a);
  else
    process (a);    /* Stop here */
}

int
bar (int a)
{
  foo (a + 5);
}
```

:::

For example, if there is a breakpoint at the commented line, here is what you might see when the program stops after executing the call `bar(0)`:

::: smallexample

```bash
(gdb) p a
$1 = 10
(gdb) p bar::a
$2 = 5
(gdb) up 2
#2  0x080483d0 in foo (a=5) at foobar.c:12
(gdb) p a
$3 = 5
(gdb) p bar::a
$4 = 0
```

:::

These uses of '`::`' are very rarely in conflict with the very similar use of the same notation in C++. When they are in conflict, the C++ meaning takes precedence; however, this can be overridden by quoting the file or function name with single quotes.

For example, suppose the program is stopped in a method of a class that has a field named `includefile`, and there is also an include file named `includefile` that defines a variable, `some_global`.

::: smallexample

```bash
(gdb) p includefile
$1 = 23
(gdb) p includefile::some_global
A syntax error in expression, near `'.
(gdb) p 'includefile'::some_global
$2 = 27
```

:::

> *Warning:* Occasionally, a local variable may appear to have the wrong value at certain points in a function---just after entry to a new scope, and just before exit.

You may see this problem when you are stepping by machine instructions. This is because, on most machines, it takes more than one instruction to set up a stack frame (including local variable definitions); if you are stepping by machine instructions, variables may appear to have the wrong values until the stack frame is completely built. On exit, it usually also takes more than one machine instruction to destroy a stack frame; after you begin stepping through that group of instructions, local variable definitions may be gone.

This may also happen when the compiler does significant optimizations. To be sure of always seeing accurate values, turn off all optimization when compiling.

Another possible effect of compiler optimizations is to optimize unused variables out of existence, or assign variables to registers (as opposed to memory addresses). Depending on the support for such cases offered by the debug info format used by the compiler, [GDB] will print a message like this:

::: smallexample

```bash
No symbol "foo" in current context.
```

:::

To solve such problems, either recompile without optimizations, or use a different debug info format, if the compiler supports several such formats. See [Compilation](Compilation.html#Compilation), for more information on choosing compiler options. See [C and C++](C.html#C), for more information about debug info formats that are best suited to C++ programs.

If you ask to print an object whose contents are unknown to [GDB]'. See [incomplete type](Symbols.html#Symbols), for more about this.

If you try to examine or use the value of a (global) variable for which [GDB] gets the variable's value using the cast-to type as the variable's type. For example, in a C program:

::: smallexample

```bash
  (gdb) p var
  'var' has unknown type; cast it to its declared type
  (gdb) p (float) var
  $1 = 3.14
```

:::

If you append [\@entry] string to a function parameter name you get its value at the time the function got called. If the value is not available an error message is printed. Entry values are available only with some compilers. Entry values are normally also printed at the function parameter list according to [set print entry-values](Print-Settings.html#set-print-entry_002dvalues).

::: smallexample

```bash
Breakpoint 1, d (i=30) at gdb.base/entry-value.c:29
29    i++;
(gdb) next
30    e (i);
(gdb) print i
$1 = 31
(gdb) print i@entry
$2 = 30
```

:::

Strings are identified as arrays of `char` values without specified signedness. Arrays of either `signed char` or `unsigned char` get printed as arrays of 1 byte sized integers. `-fsigned-char` or `-funsigned-char` [GCC] defines literal string type `"char"` as `char` without a sign. For program code

::: smallexample

```bash
char var0 = "A";
signed char var1 = "A";
```

:::

You get during debugging

::: smallexample

```bash
(gdb) print var0
$1 = "A"
(gdb) print var1
$2 = 
```

:::

---

::: header
Next: [Arrays](Arrays.html#Arrays)]
:::
