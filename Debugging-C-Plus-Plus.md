---
tip: translate by openai@2023-06-23 20:19:15
...
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

> 一些[GDB]命令特别适合用于C++，有些则专门用于C++。以下是总结：

`breakpoint menus`


When you want a breakpoint in a function whose name is overloaded, [GDB] has the capability to display a menu of possible breakpoint locations to help you specify which function definition you want. See [Ambiguous Expressions](Ambiguous-Expressions.html#Ambiguous-Expressions).

> 当您想要在一个名字被重载的函数中设置断点时，[GDB]具有显示可能断点位置的菜单的功能，以帮助您指定要使用哪个函数定义。请参阅[Ambiguous Expressions](Ambiguous-Expressions.html#Ambiguous-Expressions)。

`rbreak regex`


Setting breakpoints using regular expressions is helpful for setting breakpoints on overloaded functions that are not members of any special classes. See [Setting Breakpoints](Set-Breaks.html#Set-Breaks).

> 使用正则表达式设置断点有助于设置负载过高的函数的断点，这些函数不属于任何特殊类。请参见[设置断点](Set-Breaks.html#Set-Breaks)。

`catch throw`

`catch rethrow`

`catch catch`


Debug C++ exception handling using these commands. See [Setting Catchpoints](Set-Catchpoints.html#Set-Catchpoints).

> 调试C++异常处理，使用这些命令。参见[设置捕获点](Set-Catchpoints.html#Set-Catchpoints)。

`ptype typename`


Print inheritance relationships as well as other information for type `typename`. See [Examining the Symbol Table](Symbols.html#Symbols).

> 打印类型`typename`的继承关系以及其他信息。参见[检查符号表](Symbols.html#Symbols)。

`info vtbl expression.`


The `info vtbl` command can be used to display the virtual method tables of the object computed by `expression`. This shows one entry per virtual table; there may be multiple virtual tables when multiple inheritance is in use.

> 命令`info vtbl`可用于显示由表达式计算出的对象的虚拟方法表。这显示了每个虚拟表的一个条目；当使用多重继承时，可能有多个虚拟表。

`demangle name`


Demangle `name`. See [Symbols](Symbols.html#Symbols), for a more complete description of the `demangle` command.

> 解码“name”。有关更完整的`demangle`命令描述，请参阅[符号](Symbols.html#Symbols)。

`set print demangle`

`show print demangle`

`set print asm-demangle`

`show print asm-demangle`


Control whether C++ symbols display in their source form, both when displaying code as C++ source and when displaying disassemblies. See [Print Settings](Print-Settings.html#Print-Settings).

> 控制C++符号在显示为C++源码和显示反汇编时是否以其原始形式显示。请参见[打印设置](Print-Settings.html#Print-Settings)。

`set print object`

`show print object`


Choose whether to print derived (actual) or declared types of objects. See [Print Settings](Print-Settings.html#Print-Settings).

> 选择是打印派生（实际）类型的对象，还是打印声明的类型的对象。请参阅[打印设置](Print-Settings.html#Print-Settings)。

`set print vtbl`

`show print vtbl`


Control the format for printing virtual function tables. See [Print Settings](Print-Settings.html#Print-Settings). (The `vtbl` commands do not work on programs compiled with the HP ANSI C++ compiler (`aCC`).)

> 控制打印虚拟函数表的格式。请参阅[打印设置](Print-Settings.html#Print-Settings)。（`vtbl`命令不适用于使用HP ANSI C++编译器（`aCC`）编译的程序。）

`set overload-resolution on`


Enable overload resolution for C++ expression evaluation. The default is on. For overloaded functions, [GDB] evaluates the arguments and searches for a function whose signature matches the argument types, using the standard C++ conversion rules (see [C++ Expressions](C-Plus-Plus-Expressions.html#C-Plus-Plus-Expressions), for details). If it cannot find a match, it emits a message.

> 启用C++表达式评估的重载解析。默认情况下是开启的。对于重载函数，[GDB]会评估参数并搜索与参数类型匹配的函数，使用标准C++转换规则（详情参见[C++ Expressions](C-Plus-Plus-Expressions.html#C-Plus-Plus-Expressions)）。如果找不到匹配，它会发出一条消息。

`set overload-resolution off`


Disable overload resolution for C++ expression evaluation. For overloaded functions that are not class member functions, [GDB] searches for a function whose signature *exactly* matches the argument types.

> 禁用C++表达式求值的重载解析。对于非类成员函数的重载函数，[GDB] 搜索签名完全匹配参数类型的函数。

`show overload-resolution`

Show the current setting of overload resolution.

`Overloaded symbol names`


You can specify a particular definition of an overloaded symbol, using the same notation that is used to declare such symbols in C++: type `symbol(types)` rather than just `symbol` command-line word completion facilities to list the available choices, or to finish the type list for you. See [Command Completion](Completion.html#Completion), for details on how to do this.

> 您可以使用与在C++中声明这种符号相同的符号来指定被重载符号的特定定义：使用 `symbol(types)` 而不仅仅是 `symbol` 命令行词语完成功能来列出可用的选择，或为您完成类型列表。有关如何执行此操作的详细信息，请参阅[命令完成](Completion.html#Completion)。

`Breakpoints in template functions`


Similar to how overloaded symbols are handled, [GDB] will ignore template parameter lists when it encounters a symbol which includes a C++ template. This permits setting breakpoints on families of template functions or functions whose parameters include template types.

> 类似于如何处理超载符号，当[GDB]遇到包含C ++模板的符号时，它会忽略模板参数列表。这允许在模板函数或其参数包括模板类型的函数上设置断点。

The [-qualified] to search for a specific function or type.


The [GDB] command-line word completion facility also understands template parameters and may be used to list available choices or finish template parameter lists for you. See [Command Completion](Completion.html#Completion), for details on how to do this.

> GDB 命令行词语补全设施也能理解模板参数，可用于列出可用选择或为您完成模板参数列表。有关如何执行此操作的详细信息，请参阅[命令完成](Completion.html#Completion)。

`Breakpoints in functions with ABI tags`


The GNU C++ compiler introduced the notion of ABI "tags", which correspond to changes in the ABI of a type, function, or variable that would not otherwise be reflected in a mangled name. See [https://developers.redhat.com/blog/2015/02/05/gcc5-and-the-c11-abi/](https://developers.redhat.com/blog/2015/02/05/gcc5-and-the-c11-abi/) for more detail.

> GNU C++ 编译器引入了ABI“标签”的概念，这些标签与类型、函数或变量的ABI变化有关，而这种变化不会反映在符号名中。有关更多细节，请参见[https://developers.redhat.com/blog/2015/02/05/gcc5-and-the-c11-abi/](https://developers.redhat.com/blog/2015/02/05/gcc5-and-the-c11-abi/)。


The ABI tags are visible in C++ demangled names. For example, a function that returns a std::string:

> 在C++解码的名称中可以看到ABI标签。例如，一个返回std::string的函数：

::: smallexample

```bash
std::string function(int);
```

:::


when compiled for the C++11 ABI is marked with the `cxx11` ABI tag, and [GDB] displays the symbol like this:

> 当为C++11 ABI编译时，会带有`cxx11` ABI标记，[GDB]会这样显示符号：

::: smallexample

```bash
function[abi:cxx11](int)
```

:::


You can set a breakpoint on such functions simply as if they had no tag. For example:

> 你可以像对没有标签的函数一样简单地设置断点。例如：

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

> 在极少数情况下，您需要解开不同ABI标签之间的歧义时，可以通过简单地将ABI标签包含在函数名中来实现，例如：

::: smallexample

```bash
(gdb) b ambiguous[abi:other_tag](int)
```

:::

---

::: header
Next: [Decimal Floating Point](Decimal-Floating-Point.html#Decimal-Floating-Point)]
:::
