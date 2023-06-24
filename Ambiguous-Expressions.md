---
tip: translate by openai@2023-06-23 17:11:13
...
---
description: Ambiguous Expressions (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Ambiguous Expressions (Debugging with GDB)
lang: en
resource-type: document
title: Ambiguous Expressions (Debugging with GDB)
---
::: header
Next: [Variables](Variables.html#Variables)]
:::

---

### 10.2 Ambiguous Expressions


Expressions can sometimes contain some ambiguous elements. For instance, some programming languages (notably Ada, C++ and Objective-C) permit a single function name to be defined several times, for application in different contexts. This is called *overloading*. Another example involving Ada is generics. A *generic package* is similar to C++ templates and is typically instantiated several times, resulting in the same function name being defined in different contexts.

> 表达式有时可能包含一些模糊的元素。例如，某些编程语言（特别是Ada、C++和Objective-C）允许单个函数名被定义多次，用于不同的上下文中。这被称为*重载*。另一个涉及Ada的例子是泛型。*泛型包*类似于C++模板，通常会被多次实例化，导致相同的函数名被定义在不同的上下文中。


In some cases and depending on the language, it is possible to adjust the expression to remove the ambiguity. For instance in C++, you can specify the signature of the function you want to break on, as in [break `function`. In Ada, using the fully qualified name of your function often makes the expression unambiguous as well.

> 在某些情况下，取决于语言，可以调整表达式以消除歧义。例如，在C++中，可以指定要断开的函数的签名，如[break`function`]。在Ada中，使用完全限定的函数名称通常也可以使表达式不易混淆。


When an ambiguity that needs to be resolved is detected, the debugger has the capability to display a menu of numbered choices for each possibility, and then waits for the selection with the prompt '`>` selects all possible choices.

> 当检测到需要解决的歧义时，调试器具有显示每个可能性的编号菜单的能力，然后等待用'>'提示的选择，以选择所有可能的选择。


For example, the following session excerpt shows an attempt to set a breakpoint at the overloaded symbol `String::after`. We choose three particular definitions of that function name:

> 例如，以下会话摘录显示了尝试在被重载的符号“String :: after”处设置断点的尝试。我们选择该函数名称的三个特定定义：

::: smallexample

```bash
(gdb) b String::after
[0] cancel
[1] all
[2] file:String.cc; line number:867
[3] file:String.cc; line number:860
[4] file:String.cc; line number:875
[5] file:String.cc; line number:853
[6] file:String.cc; line number:846
[7] file:String.cc; line number:735
> 2 4 6
Breakpoint 1 at 0xb26c: file String.cc, line 867.
Breakpoint 2 at 0xb344: file String.cc, line 875.
Breakpoint 3 at 0xafcc: file String.cc, line 846.
Multiple breakpoints were set.
Use the "delete" command to delete unwanted
 breakpoints.
(gdb)
```

:::

`set multiple-symbols mode`


This option allows you to adjust the debugger behavior when an expression is ambiguous.

> 此选项允许您在表达式不明确时调整调试器行为。


By default, `mode` uses the menu to help you disambiguate the expression. For instance, printing the address of an overloaded function will result in the use of the menu.

> 默认情况下，`mode`使用菜单帮助您消除歧义表达。例如，打印重载函数的地址将导致使用菜单。


When `mode` is set to `ask`, the debugger always uses the menu when an ambiguity is detected.

> 当模式设置为“ask”时，调试器在检测到歧义时总是使用菜单。


Finally, when `mode` is set to `cancel`, the debugger reports an error due to the ambiguity and the command is aborted.

> 最后，当`模式`设置为`取消`时，由于模糊性，调试器会报告错误，并中止命令。

`show multiple-symbols`


Show the current value of the `multiple-symbols` setting.

> 显示`multiple-symbols`设置的当前值。

---

::: header
Next: [Variables](Variables.html#Variables)]
:::
