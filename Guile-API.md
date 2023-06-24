---
tip: translate by openai@2023-06-23 22:57:36
...
---
description: Guile API (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Guile API (Debugging with GDB)
lang: en
resource-type: document
title: Guile API (Debugging with GDB)
---
::: header
Next: [Guile Auto-loading](Guile-Auto_002dloading.html#Guile-Auto_002dloading)]
:::

---

#### 23.4.3 Guile API


You can get quick online help for [GDB] from the Guile interactive prompt.

> 你可以从Guile交互提示符中快速获得[GDB]的在线帮助。

---


• [Basic Guile](Basic-Guile.html#Basic-Guile):                                                                            Basic Guile Functions

> • [基本欺骗](Basic-Guile.html#Basic-Guile):                                                                            基本欺骗功能

• [Guile Configuration](Guile-Configuration.html#Guile-Configuration):                                                    Guile configuration variables

> • [Guile 配置](Guile-Configuration.html#Guile-Configuration):  Guile 配置变量

• [GDB Scheme Data Types](GDB-Scheme-Data-Types.html#GDB-Scheme-Data-Types):                                              Scheme representations of GDB objects

> • [GDB Scheme 数据类型](GDB-Scheme-Data-Types.html#GDB-Scheme-Data-Types):                                              GDB 对象的 Scheme 表示

• [Guile Exception Handling](Guile-Exception-Handling.html#Guile-Exception-Handling):                                     How Guile exceptions are translated

> • [Guile 异常处理](Guile-Exception-Handling.html#Guile-Exception-Handling):                                   Guile 如何转译异常

• [Values From Inferior In Guile](Values-From-Inferior-In-Guile.html#Values-From-Inferior-In-Guile):                      Guile representation of values

> • [Guile中的次级值](Values-From-Inferior-In-Guile.html#Values-From-Inferior-In-Guile): Guile表示的值

• [Arithmetic In Guile](Arithmetic-In-Guile.html#Arithmetic-In-Guile):                                                    Arithmetic in Guile

> •[Guile中的算术](Arithmetic-In-Guile.html#Arithmetic-In-Guile):  算术在Guile中

• [Types In Guile](Types-In-Guile.html#Types-In-Guile):                                                                   Guile representation of types

> • [Guile中的类型](Types-In-Guile.html#Types-In-Guile):                                                                   Guile表示类型

• [Guile Pretty Printing API](Guile-Pretty-Printing-API.html#Guile-Pretty-Printing-API):                                  Pretty-printing values with Guile

> • [Guile 美化打印 API](Guile-Pretty-Printing-API.html#Guile-Pretty-Printing-API): 使用 Guile 美化打印值

• [Selecting Guile Pretty-Printers](Selecting-Guile-Pretty_002dPrinters.html#Selecting-Guile-Pretty_002dPrinters):        How GDB chooses a pretty-printer

> • [选择 Guile Pretty-Printers](Selecting-Guile-Pretty_002dPrinters.html#Selecting-Guile-Pretty_002dPrinters):    如何 GDB 选择一个漂亮的打印机？

• [Writing a Guile Pretty-Printer](Writing-a-Guile-Pretty_002dPrinter.html#Writing-a-Guile-Pretty_002dPrinter):                          Writing a pretty-printer

> • [编写Guile Pretty-Printer](Writing-a-Guile-Pretty_002dPrinter.html#Writing-a-Guile-Pretty_002dPrinter):                   编写一个漂亮的打印机

• [Commands In Guile](Commands-In-Guile.html#Commands-In-Guile):                                                                         Implementing new commands in Guile

> • [Guile中的命令](Commands-In-Guile.html#Commands-In-Guile): 在Guile中实现新的命令

• [Parameters In Guile](Parameters-In-Guile.html#Parameters-In-Guile):                                                                   Adding new [GDB] parameters

> • [Guile 中的参数](Parameters-In-Guile.html#Parameters-In-Guile):                                                                   添加新的 [GDB] 参数

• [Progspaces In Guile](Progspaces-In-Guile.html#Progspaces-In-Guile):                                                                   Program spaces

> • [Guile中的程序空间](Progspaces-In-Guile.html#Progspaces-In-Guile): 程序空间

• [Objfiles In Guile](Objfiles-In-Guile.html#Objfiles-In-Guile):                                                                         Object files in Guile

> • [在Guile中的对象文件](Objfiles-In-Guile.html#Objfiles-In-Guile):                                                                         在Guile中的对象文件

• [Frames In Guile](Frames-In-Guile.html#Frames-In-Guile):                                                                               Accessing inferior stack frames from Guile

> • [Guile中的框架](Frames-In-Guile.html#Frames-In-Guile): 从Guile访问较低层次的堆栈框架

• [Blocks In Guile](Blocks-In-Guile.html#Blocks-In-Guile):                                                                               Accessing blocks from Guile

> • [在Guile中的块](Blocks-In-Guile.html#Blocks-In-Guile): 从Guile访问块

• [Symbols In Guile](Symbols-In-Guile.html#Symbols-In-Guile):                                                                            Guile representation of symbols

> • [Guile中的符号](Symbols-In-Guile.html#Symbols-In-Guile): Guile表示的符号

• [Symbol Tables In Guile](Symbol-Tables-In-Guile.html#Symbol-Tables-In-Guile):                                                          Guile representation of symbol tables

> • [在Guile中的符号表](Symbol-Tables-In-Guile.html#Symbol-Tables-In-Guile): Guile表示符号表

• [Breakpoints In Guile](Breakpoints-In-Guile.html#Breakpoints-In-Guile):                                                                Manipulating breakpoints using Guile

> • [Guile中的断点](Breakpoints-In-Guile.html#Breakpoints-In-Guile): 使用Guile操纵断点

• [Lazy Strings In Guile](Lazy-Strings-In-Guile.html#Lazy-Strings-In-Guile):                                                             Guile representation of lazy strings

> • [Guile中的惰性字符串](Lazy-Strings-In-Guile.html#Lazy-Strings-In-Guile): Guile表示惰性字符串。

• [Architectures In Guile](Architectures-In-Guile.html#Architectures-In-Guile):                                                          Guile representation of architectures

> • [Guile中的架构](Architectures-In-Guile.html#Architectures-In-Guile): Guile对架构的表示

• [Disassembly In Guile](Disassembly-In-Guile.html#Disassembly-In-Guile):                                                                Disassembling instructions from Guile

> • [在Guile中反汇编](Disassembly-In-Guile.html#Disassembly-In-Guile): 从Guile中反汇编指令

• [I/O Ports in Guile](I_002fO-Ports-in-Guile.html#I_002fO-Ports-in-Guile):                                                              GDB I/O ports

> • [Guile中的I/O端口](I_002fO-Ports-in-Guile.html#I_002fO-Ports-in-Guile)：GDB I/O端口

• [Memory Ports in Guile](Memory-Ports-in-Guile.html#Memory-Ports-in-Guile):                                                             Accessing memory through ports and bytevectors

> • [Guile中的内存端口](Memory-Ports-in-Guile.html#Memory-Ports-in-Guile): 通过端口和字节向量访问内存

• [Iterators In Guile](Iterators-In-Guile.html#Iterators-In-Guile):                                                                      Basic iterator support

> • [Guile中的迭代器](Iterators-In-Guile.html#Iterators-In-Guile):                                                                   基本迭代器支持

---

---

::: header
Next: [Guile Auto-loading](Guile-Auto_002dloading.html#Guile-Auto_002dloading)]
:::
