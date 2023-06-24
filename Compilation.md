---
tip: translate by openai@2023-06-23 19:19:55
...
---
description: Compilation (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Compilation (Debugging with GDB)
lang: en
resource-type: document
title: Compilation (Debugging with GDB)
---
::: header
Next: [Starting](Starting.html#Starting)]
:::

---

### 4.1 Compiling for Debugging


In order to debug a program effectively, you need to generate debugging information when you compile it. This debugging information is stored in the object file; it describes the data type of each variable or function and the correspondence between source line numbers and addresses in the executable code.

> 要有效地调试程序，您需要在编译时生成调试信息。此调试信息存储在对象文件中；它描述每个变量或函数的数据类型以及源代码行号与可执行代码中地址之间的对应关系。


To request debugging information, specify the '`-g`' option when you run the compiler.

> 要请求调试信息，在运行编译器时指定 '-g' 选项。


Programs that are to be shipped to your customers are compiled with optimizations, using the '`-O`' options together. Using those compilers, you cannot generate optimized executables containing debugging information.

> 客户收到的程序使用`-O`选项进行优化编译，使用这些编译器，您无法生成包含调试信息的优化可执行文件。


[GCC]' whenever you compile a program. You may think your program is correct, but there is no sense in pushing your luck. For more information, see [Optimized Code](Optimized-Code.html#Optimized-Code).

> 每当你编译一个程序时，请使用[GCC]。你可能认为你的程序没有错误，但是不要冒险。要了解更多信息，请参见[优化代码](Optimized-Code.html#Optimized-Code)。

Older versions of the [GNU] C compiler has this option, do not use it.

[GDB].


See [Options for Debugging Your Program or GCC](http://gcc.gnu.org/onlinedocs/gcc/Debugging-Options.html#Debugging-Options) in Using the [GNU] options affecting debug information.

> 请参阅[GNU调试信息影响选项](http://gcc.gnu.org/onlinedocs/gcc/Debugging-Options.html#Debugging-Options)，以了解有关调试程序或GCC的选项。


You will have the best debugging experience if you use the latest version of the DWARF debugging format that your compiler supports. DWARF is currently the most expressive and best supported debugging format in [GDB].

> 如果您使用编译器支持的最新版本的DWARF调试格式，您将获得最佳的调试体验。 DWARF目前是[GDB]中表达能力最强，支持最好的调试格式。

---

::: header
Next: [Starting](Starting.html#Starting)]
:::
