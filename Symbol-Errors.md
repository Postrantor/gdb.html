---
tip: translate by openai@2023-06-24 03:26:34
...
---
description: Symbol Errors (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Symbol Errors (Debugging with GDB)
lang: en
resource-type: document
title: Symbol Errors (Debugging with GDB)
---
::: header
Next: [Data Files](Data-Files.html#Data-Files)]
:::

---

### 18.6 Errors Reading Symbol Files


While reading a symbol file, [GDB] to print more messages, to see how many times the problems occur, with the `set complaints` command (see [Optional Warnings and Messages](Messages_002fWarnings.html#Messages_002fWarnings)).

> 当读取符号文件时，[GDB] 可以使用 `set complaints` 命令（参见[可选警告和消息](Messages_002fWarnings.html#Messages_002fWarnings)）打印更多消息，以查看问题发生的次数。

The messages currently printed, and their meanings, include:

`inner block not inside outer block in symbol`


:   The symbol information shows where symbol scopes begin and end (such as at the start of a function or a block of statements). This error indicates that an inner scope block is not fully contained in its outer scope blocks.

> 符号信息显示符号范围从何处开始和结束（例如在函数开始或一组语句块开始时）。此错误表明内部范围块未完全包含在其外部范围块中。

```
[GDB] may be shown as "`(don't know)`" if the outer block is not a function.
```

`block at address out of order`


:   The symbol information for symbol scope blocks should occur in order of increasing addresses. This error indicates that it does not do so.

> 这个错误表明，符号范围块的符号信息应该按照地址递增的顺序出现。

```
[GDB] does not circumvent this problem, and has trouble locating symbols in the source file whose symbols it is reading. (You can often determine what source file is affected by specifying `set verbose on`. See [Optional Warnings and Messages](Messages_002fWarnings.html#Messages_002fWarnings).)
```

`bad block start address patched`


:   The symbol information for a symbol scope block has a start address smaller than the address of the preceding source line. This is known to occur in the SunOS 4.1.1 (and earlier) C compiler.

> 符号范围块的符号信息具有比前面源代码行地址更小的起始地址。这在SunOS 4.1.1（及以前）的C编译器中是已知的。

```
[GDB] circumvents the problem by treating the symbol scope block as starting on the previous source line.
```

`bad string table offset in symbol n`

:

```
Symbol number `n` contains a pointer into the string table which is larger than the size of the string table.

[GDB] circumvents the problem by considering the symbol to have the name `foo`, which may cause other problems if many symbols end up with this name.
```

`unknown symbol type 0xnn`


:   The symbol information contains new data types that [GDB] does not yet know how to read. `0xnn` is the symbol type of the uncomprehended information, in hexadecimal.

> 符号信息包含[GDB]尚不知道如何读取的新数据类型。`0xnn`是未理解信息的符号类型，以十六进制表示。

```
[GDB] circumvents the error by ignoring this symbol information. This usually allows you to debug your program, though certain symbols are not accessible. If you encounter such a problem and feel like debugging it, you can debug `gdb` with itself, breakpoint on `complain`, then go up to the function `read_dbx_symtab` and examine `*bufp` to see the symbol.
```

`stub type has NULL name`

:   [GDB] could not find the full definition for a struct or class.

`const/volatile indicator missing (ok if using g++ v1.x), got…`


:   The symbol information for a C++ member function is missing some information that recent versions of the compiler should have output for it.

> 编译器应该为C++成员函数输出的符号信息缺少一些最新版本应有的信息。

`info mismatch between compiler and debugger`

:   [GDB] could not parse a type specification output by the compiler.

---

::: header
Next: [Data Files](Data-Files.html#Data-Files)]
:::
