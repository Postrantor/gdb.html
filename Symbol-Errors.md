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

The messages currently printed, and their meanings, include:

`inner block not inside outer block in symbol`

:   The symbol information shows where symbol scopes begin and end (such as at the start of a function or a block of statements). This error indicates that an inner scope block is not fully contained in its outer scope blocks.

```
[GDB] may be shown as "`(don't know)`" if the outer block is not a function.
```

`block at address out of order`

:   The symbol information for symbol scope blocks should occur in order of increasing addresses. This error indicates that it does not do so.

```
[GDB] does not circumvent this problem, and has trouble locating symbols in the source file whose symbols it is reading. (You can often determine what source file is affected by specifying `set verbose on`. See [Optional Warnings and Messages](Messages_002fWarnings.html#Messages_002fWarnings).)
```

`bad block start address patched`

:   The symbol information for a symbol scope block has a start address smaller than the address of the preceding source line. This is known to occur in the SunOS 4.1.1 (and earlier) C compiler.

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

```
[GDB] circumvents the error by ignoring this symbol information. This usually allows you to debug your program, though certain symbols are not accessible. If you encounter such a problem and feel like debugging it, you can debug `gdb` with itself, breakpoint on `complain`, then go up to the function `read_dbx_symtab` and examine `*bufp` to see the symbol.
```

`stub type has NULL name`

:   [GDB] could not find the full definition for a struct or class.

`const/volatile indicator missing (ok if using g++ v1.x), got…`

:   The symbol information for a C++ member function is missing some information that recent versions of the compiler should have output for it.

`info mismatch between compiler and debugger`

:   [GDB] could not parse a type specification output by the compiler.

---

::: header
Next: [Data Files](Data-Files.html#Data-Files)]
:::
