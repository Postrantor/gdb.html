---
tip: translate by openai@2023-06-24 01:35:49
...
---
description: Python API (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Python API (Debugging with GDB)
lang: en
resource-type: document
title: Python API (Debugging with GDB)
---
::: header
Next: [Python Auto-loading](Python-Auto_002dloading.html#Python-Auto_002dloading)]
:::

---

#### 23.3.2 Python API

You can get quick online help for [GDB].


Functions and methods which have two or more optional arguments allow them to be specified using keyword syntax. This allows passing some optional arguments while skipping others. Example: `gdb.some_function ('foo', bar = 1, baz = 2)`.

> 函数和方法具有两个或多个可选参数时，可以使用关键字语法来指定它们。这允许在跳过其他参数的同时传递一些可选参数。例如：`gdb.some_function（'foo'，bar = 1，baz = 2）`。

---


• [Basic Python](Basic-Python.html#Basic-Python):                                                       Basic Python Functions.

> • [基础Python](Basic-Python.html#Basic-Python):基础Python函数。

• [Exception Handling](Exception-Handling.html#Exception-Handling):                                     How Python exceptions are translated.

> • [异常处理](Exception-Handling.html#Exception-Handling)：Python异常的翻译。

• [Values From Inferior](Values-From-Inferior.html#Values-From-Inferior):                               Python representation of values.

> • [从劣质中获取价值](Values-From-Inferior.html#Values-From-Inferior): 从Python表示的值中提取。

• [Types In Python](Types-In-Python.html#Types-In-Python):                                              Python representation of types.

> •[Python中的类型](Types-In-Python.html#Types-In-Python):Python表示类型。

• [Pretty Printing API](Pretty-Printing-API.html#Pretty-Printing-API):                                  Pretty-printing values.

> • [Pretty Printing API](Pretty-Printing-API.html#Pretty-Printing-API): 美化打印值。

• [Selecting Pretty-Printers](Selecting-Pretty_002dPrinters.html#Selecting-Pretty_002dPrinters):        How GDB chooses a pretty-printer.

> • [选择 Pretty-Printers](Selecting-Pretty_002dPrinters.html#Selecting-Pretty_002dPrinters):        GDB如何选择一个pretty-printer。

• [Writing a Pretty-Printer](Writing-a-Pretty_002dPrinter.html#Writing-a-Pretty_002dPrinter):           Writing a Pretty-Printer.

> 写一个漂亮的打印机：写一个漂亮的打印机。

• [Type Printing API](Type-Printing-API.html#Type-Printing-API):                                        Pretty-printing types.

> • [类型打印API](Type-Printing-API.html#Type-Printing-API): 美观的打印类型。

• [Frame Filter API](Frame-Filter-API.html#Frame-Filter-API):                                           Filtering Frames.

> • [帧过滤器 API](Frame-Filter-API.html#Frame-Filter-API)：过滤帧。

• [Frame Decorator API](Frame-Decorator-API.html#Frame-Decorator-API):                                                 Decorating Frames.

> • [框架装饰器 API](Frame-Decorator-API.html#Frame-Decorator-API):  装饰框架。

• [Writing a Frame Filter](Writing-a-Frame-Filter.html#Writing-a-Frame-Filter):                                        Writing a Frame Filter.

> • [编写帧过滤器](Writing-a-Frame-Filter.html#Writing-a-Frame-Filter): 编写帧过滤器。

• [Unwinding Frames in Python](Unwinding-Frames-in-Python.html#Unwinding-Frames-in-Python):                            Writing frame unwinder.

> • [Python中的解开框架](Unwinding-Frames-in-Python.html#Unwinding-Frames-in-Python): 写框架解开器。

• [Xmethods In Python](Xmethods-In-Python.html#Xmethods-In-Python):                                                    Adding and replacing methods of C++ classes.

> • [Python中的X方法](Xmethods-In-Python.html#Xmethods-In-Python): 添加和替换C++类的方法。

• [Xmethod API](Xmethod-API.html#Xmethod-API):                                                                         Xmethod types.

> • [Xmethod API](Xmethod-API.html#Xmethod-API): Xmethod 类型。

• [Writing an Xmethod](Writing-an-Xmethod.html#Writing-an-Xmethod):                                                    Writing an xmethod.

> • [书写X方法](Writing-an-Xmethod.html#Writing-an-Xmethod): 书写X方法。

• [Inferiors In Python](Inferiors-In-Python.html#Inferiors-In-Python):                                                 Python representation of inferiors (processes)

> • [Python中的下属](Inferiors-In-Python.html#Inferiors-In-Python):  Python表示的下属（进程）

• [Events In Python](Events-In-Python.html#Events-In-Python):                                                          Listening for events from [GDB].

> • [Python中的事件](Events-In-Python.html#Events-In-Python): 从[GDB]中侦听事件。

• [Threads In Python](Threads-In-Python.html#Threads-In-Python):                                                       Accessing inferior threads from Python.

> • [Python中的线程](Threads-In-Python.html#Threads-In-Python): 从Python访问次级线程。

• [Recordings In Python](Recordings-In-Python.html#Recordings-In-Python):                                              Accessing recordings from Python.

> • [Python中的录音](Recordings-In-Python.html#Recordings-In-Python): 从Python访问录音。

• [CLI Commands In Python](CLI-Commands-In-Python.html#CLI-Commands-In-Python):                                        Implementing new CLI commands in Python.

> • [在Python中的CLI命令](CLI-Commands-In-Python.html#CLI-Commands-In-Python):                                        在Python中实现新的CLI命令。

• [GDB/MI Commands In Python](GDB_002fMI-Commands-In-Python.html#GDB_002fMI-Commands-In-Python):                       Implementing new [GDB/MI] commands in Python.

> •[在Python中使用GDB / MI命令](GDB_002fMI-Commands-In-Python.html#GDB_002fMI-Commands-In-Python): 使用Python实现新的[GDB / MI]命令。

• [Parameters In Python](Parameters-In-Python.html#Parameters-In-Python):                                              Adding new [GDB] parameters.

> • [Python 中的参数](Parameters-In-Python.html#Parameters-In-Python): 添加新的[GDB]参数。

• [Functions In Python](Functions-In-Python.html#Functions-In-Python):                                                 Writing new convenience functions.

> • [Python 中的函数](Functions-In-Python.html#Functions-In-Python)：写新的便利函数。

• [Progspaces In Python](Progspaces-In-Python.html#Progspaces-In-Python):                                              Program spaces.

> • [Python中的程序空间](Progspaces-In-Python.html#Progspaces-In-Python): 程序空间。

• [Objfiles In Python](Objfiles-In-Python.html#Objfiles-In-Python):                                                    Object files.

> • [Python中的Objfiles](Objfiles-In-Python.html#Objfiles-In-Python): 对象文件。

• [Frames In Python](Frames-In-Python.html#Frames-In-Python):                                                          Accessing inferior stack frames from Python.

> • [Python中的框架](Frames-In-Python.html#Frames-In-Python): 从Python访问较低层次的堆栈框架。

• [Blocks In Python](Blocks-In-Python.html#Blocks-In-Python):                                                          Accessing blocks from Python.

> • [在Python中的块](Blocks-In-Python.html#Blocks-In-Python): 从Python访问块。

• [Symbols In Python](Symbols-In-Python.html#Symbols-In-Python):                                                       Python representation of symbols.

> • [Python中的符号](Symbols-In-Python.html#Symbols-In-Python): Python表示的符号。

• [Symbol Tables In Python](Symbol-Tables-In-Python.html#Symbol-Tables-In-Python):                                     Python representation of symbol tables.

> • [Python中的符号表](Symbol-Tables-In-Python.html#Symbol-Tables-In-Python): Python表示符号表。

• [Line Tables In Python](Line-Tables-In-Python.html#Line-Tables-In-Python):                                           Python representation of line tables.

> • [Python中的线表](Line-Tables-In-Python.html#Line-Tables-In-Python): Python线表的表示。

• [Breakpoints In Python](Breakpoints-In-Python.html#Breakpoints-In-Python):                                           Manipulating breakpoints using Python.

> • [Python中的断点](Breakpoints-In-Python.html#Breakpoints-In-Python): 使用Python操纵断点。

• [Finish Breakpoints in Python](Finish-Breakpoints-in-Python.html#Finish-Breakpoints-in-Python):                      Setting Breakpoints on function return using Python.

> • [在Python中完成断点](Finish-Breakpoints-in-Python.html#Finish-Breakpoints-in-Python): 使用Python在函数返回时设置断点。

• [Lazy Strings In Python](Lazy-Strings-In-Python.html#Lazy-Strings-In-Python):                                        Python representation of lazy strings.

> •[Python中的惰性字符串](Lazy-Strings-In-Python.html#Lazy-Strings-In-Python): Python表示惰性字符串。

• [Architectures In Python](Architectures-In-Python.html#Architectures-In-Python):                                     Python representation of architectures.

> • [Python中的架构](Architectures-In-Python.html#Architectures-In-Python): Python表示的架构。

• [Registers In Python](Registers-In-Python.html#Registers-In-Python):                                                 Python representation of registers.

> • [Python中的寄存器](Registers-In-Python.html#Registers-In-Python): Python对寄存器的表示。

• [Connections In Python](Connections-In-Python.html#Connections-In-Python):                                           Python representation of connections.

> • [Python中的连接](Connections-In-Python.html#Connections-In-Python)：Python 表示的连接。

• [TUI Windows In Python](TUI-Windows-In-Python.html#TUI-Windows-In-Python):                                           Implementing new TUI windows.

> • [TUI Windows In Python](TUI-Windows-In-Python.html#TUI-Windows-In-Python): 实现新的TUI窗口。

• [Disassembly In Python](Disassembly-In-Python.html#Disassembly-In-Python):                                           Instruction Disassembly In Python

> • [在Python中反汇编](Disassembly-In-Python.html#Disassembly-In-Python):                                    指令反汇编在Python中

---

---

::: header
Next: [Python Auto-loading](Python-Auto_002dloading.html#Python-Auto_002dloading)]
:::
