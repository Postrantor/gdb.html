---
description: Debugging C Plus Plus (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Debugging C Plus Plus (Debugging with GDB)
lang: en
resource-type: document
title: Debugging C Plus Plus (Debugging with GDB)
---
::: header
Next: [Decimal Floating Point](Decimal-Floating-Point.html#Decimal-Floating-Point)]
:::

---

#### 15.4.1.7 [GDB]

Some [GDB] commands are particularly useful with C++, and some are designed specifically for use with C++. Here is a summary:

`breakpoint menus`

When you want a breakpoint in a function whose name is overloaded, [GDB] has the capability to display a menu of possible breakpoint locations to help you specify which function definition you want. See [Ambiguous Expressions](Ambiguous-Expressions.html#Ambiguous-Expressions).

`rbreak regex`

Setting breakpoints using regular expressions is helpful for setting breakpoints on overloaded functions that are not members of any special classes. See [Setting Breakpoints](Set-Breaks.html#Set-Breaks).

`catch throw`

`catch rethrow`

`catch catch`

Debug C++ exception handling using these commands. See [Setting Catchpoints](Set-Catchpoints.html#Set-Catchpoints).

`ptype typename`

Print inheritance relationships as well as other information for type `typename`. See [Examining the Symbol Table](Symbols.html#Symbols).

`info vtbl expression.`

The `info vtbl` command can be used to display the virtual method tables of the object computed by `expression`. This shows one entry per virtual table; there may be multiple virtual tables when multiple inheritance is in use.

`demangle name`

Demangle `name`. See [Symbols](Symbols.html#Symbols), for a more complete description of the `demangle` command.

`set print demangle`

`show print demangle`

`set print asm-demangle`

`show print asm-demangle`

Control whether C++ symbols display in their source form, both when displaying code as C++ source and when displaying disassemblies. See [Print Settings](Print-Settings.html#Print-Settings).

`set print object`

`show print object`

Choose whether to print derived (actual) or declared types of objects. See [Print Settings](Print-Settings.html#Print-Settings).

`set print vtbl`

`show print vtbl`

Control the format for printing virtual function tables. See [Print Settings](Print-Settings.html#Print-Settings). (The `vtbl` commands do not work on programs compiled with the HP ANSI C++ compiler (`aCC`).)

`set overload-resolution on`

Enable overload resolution for C++ expression evaluation. The default is on. For overloaded functions, [GDB] evaluates the arguments and searches for a function whose signature matches the argument types, using the standard C++ conversion rules (see [C++ Expressions](C-Plus-Plus-Expressions.html#C-Plus-Plus-Expressions), for details). If it cannot find a match, it emits a message.

`set overload-resolution off`

Disable overload resolution for C++ expression evaluation. For overloaded functions that are not class member functions, [GDB] searches for a function whose signature *exactly* matches the argument types.

`show overload-resolution`

Show the current setting of overload resolution.

`Overloaded symbol names`

You can specify a particular definition of an overloaded symbol, using the same notation that is used to declare such symbols in C++: type `symbol(types)` rather than just `symbol` command-line word completion facilities to list the available choices, or to finish the type list for you. See [Command Completion](Completion.html#Completion), for details on how to do this.

`Breakpoints in template functions`

Similar to how overloaded symbols are handled, [GDB] will ignore template parameter lists when it encounters a symbol which includes a C++ template. This permits setting breakpoints on families of template functions or functions whose parameters include template types.

The [-qualified] to search for a specific function or type.

The [GDB] command-line word completion facility also understands template parameters and may be used to list available choices or finish template parameter lists for you. See [Command Completion](Completion.html#Completion), for details on how to do this.

`Breakpoints in functions with ABI tags`

The GNU C++ compiler introduced the notion of ABI "tags", which correspond to changes in the ABI of a type, function, or variable that would not otherwise be reflected in a mangled name. See [https://developers.redhat.com/blog/2015/02/05/gcc5-and-the-c11-abi/](https://developers.redhat.com/blog/2015/02/05/gcc5-and-the-c11-abi/) for more detail.

The ABI tags are visible in C++ demangled names. For example, a function that returns a std::string:

::: smallexample

```bash
std::string function(int);
```

:::

when compiled for the C++11 ABI is marked with the `cxx11` ABI tag, and [GDB] displays the symbol like this:

::: smallexample

```bash
function[abi:cxx11](int)
```

:::

You can set a breakpoint on such functions simply as if they had no tag. For example:

::: smallexample

```bash
(gdb) b function(int)
Breakpoint 2 at 0x40060d: file main.cc, line 10.
(gdb) info breakpoints
Num     Type           Disp Enb Address    What
1       breakpoint     keep y   0x0040060d in function[abi:cxx11](int)
                                           at main.cc:10
```

:::

On the rare occasion you need to disambiguate between different ABI tags, you can do so by simply including the ABI tag in the function name, like:

::: smallexample

```bash
(gdb) b ambiguous[abi:other_tag](int)
```

:::

---

::: header
Next: [Decimal Floating Point](Decimal-Floating-Point.html#Decimal-Floating-Point)]
:::
