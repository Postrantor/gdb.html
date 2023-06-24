---
tip: translate by openai@2023-06-24 04:42:32
...
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

> 最常用的表达方式是程序中变量的名称。


Variables in expressions are understood in the selected stack frame (see [Selecting a Frame](Selection.html#Selection)); they must be either:

> 在表达式中，变量是按照所选择的堆栈帧理解的（参见[选择帧] (Selection.html#Selection))；它们必须是：

- global (or file-static)

or


- visible according to the scope rules of the programming language from the point of execution in that frame

> 根据编程语言的作用域规则，在该框架中可见

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

> 你可以在函数`foo`执行时检查和使用变量`a`，但是你只能在声明变量`b`的块中执行程序时使用或检查变量`b`。


There is an exception: you can refer to a variable or function whose scope is a single source file even if the current execution point is not in this file. But it is possible to have more than one such variable or function with the same name (in different source files). If that happens, referring to that name has unpredictable effects. If you wish, you can specify a static variable in a particular function or file by using the colon-colon (`::`) notation:

> 除外情况：即使当前执行点不在该文件中，也可以引用范围仅限于单个源文件的变量或函数。但是可能存在多个具有相同名称的变量或函数（在不同的源文件中）。如果发生这种情况，引用该名称的效果是不可预测的。如果需要，可以使用冒号冒号（`::`）符号指定特定函数或文件中的静态变量：

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

> ::符号通常用于引用静态变量，因为通常通过选择适当的框架并使用变量的简单名称来消除函数中局部变量的歧义。但是，您也可以使用此符号引用封装所选框架的局部变量：

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

> 例如，如果在被注释的行处有一个断点，在执行调用`bar（0）`后，这是您可能会看到的内容：

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

> 这种使用“`”的情况很少与C++中相同符号的使用发生冲突。当它们发生冲突时，C++的意义优先；但是，可以通过用单引号引用文件或函数名来覆盖它。


For example, suppose the program is stopped in a method of a class that has a field named `includefile`, and there is also an include file named `includefile` that defines a variable, `some_global`.

> 例如，假设程序在一个具有名为`includefile`的字段的类的方法中停止，并且还有一个名为`includefile`的包含文件，它定义了一个变量`some_global`。

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

> 可能在按机器指令一步步走时会遇到这个问题。这是因为，在大多数机器上，建立一个堆栈帧（包括本地变量定义）需要不止一条指令；如果按照机器指令一步步走，变量的值可能会显示不正确，直到堆栈帧完全建立完成。在退出时，也通常需要不止一条机器指令来销毁堆栈帧；开始走这组指令之后，本地变量定义可能就不见了。


This may also happen when the compiler does significant optimizations. To be sure of always seeing accurate values, turn off all optimization when compiling.

> 编译器进行大量优化时也可能发生这种情况。为了确保始终看到准确的值，请在编译时关闭所有优化。


Another possible effect of compiler optimizations is to optimize unused variables out of existence, or assign variables to registers (as opposed to memory addresses). Depending on the support for such cases offered by the debug info format used by the compiler, [GDB] will print a message like this:

> 编译器优化的另一个可能的效果是优化未使用的变量，或将变量分配到寄存器（而不是内存地址）。根据编译器使用的调试信息格式提供的这种情况的支持，[GDB]将打印类似这样的消息：

::: smallexample

```bash
No symbol "foo" in current context.
```

:::


To solve such problems, either recompile without optimizations, or use a different debug info format, if the compiler supports several such formats. See [Compilation](Compilation.html#Compilation), for more information on choosing compiler options. See [C and C++](C.html#C), for more information about debug info formats that are best suited to C++ programs.

> 解决此类问题，可以重新编译而不使用优化，或者如果编译器支持多种调试信息格式，则使用不同的调试信息格式。有关选择编译器选项的更多信息，请参阅[编译](Compilation.html#Compilation)。有关最适合C++程序的调试信息格式的更多信息，请参阅[C和C++](C.html#C)。


If you ask to print an object whose contents are unknown to [GDB]'. See [incomplete type](Symbols.html#Symbols), for more about this.

> 如果您要求打印一个内容对[GDB]来说是未知的对象，请参阅[incomplete type](Symbols.html#Symbols)以获取更多信息。


If you try to examine or use the value of a (global) variable for which [GDB] gets the variable's value using the cast-to type as the variable's type. For example, in a C program:

> 如果你试图检查或使用（全局）变量的值，[GDB]会使用转换类型作为变量的类型来获取变量的值。例如，在C程序中：

::: smallexample

```bash
  (gdb) p var
  'var' has unknown type; cast it to its declared type
  (gdb) p (float) var
  $1 = 3.14
```

:::


If you append [\@entry] string to a function parameter name you get its value at the time the function got called. If the value is not available an error message is printed. Entry values are available only with some compilers. Entry values are normally also printed at the function parameter list according to [set print entry-values](Print-Settings.html#set-print-entry_002dvalues).

> 如果把[\@entry]字符串附加到函数参数名称，那么您就可以在调用函数时获取其值。如果值不可用，则会打印错误消息。仅有一些编译器可以获取条目值。条目值通常也会根据[set print entry-values](Print-Settings.html#set-print-entry_002dvalues)打印在函数参数列表中。

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

> 字符串被视为没有指定符号的字符数组。符号字符数组或无符号字符数组会被打印为1字节大小的整数数组。GCC中的`-fsigned-char`或`-funsigned-char`定义了字面字符串类型“char”为无符号的字符。对于程序代码

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
