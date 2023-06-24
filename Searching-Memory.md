---
tip: translate by openai@2023-06-24 02:19:45
...
---
description: Searching Memory (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Searching Memory (Debugging with GDB)
lang: en
resource-type: document
title: Searching Memory (Debugging with GDB)
---
::: header
Next: [Value Sizes](Value-Sizes.html#Value-Sizes)]
:::

---

### 10.23 Search Memory


Memory can be searched for a particular sequence of bytes with the `find` command.

> 可以使用 `find` 命令在内存中搜索特定字节序列。

`find [/sn] start_addr, +len, val1 [, val2, …]`

`find [/sn] start_addr, end_addr, val1 [, val2, …]`

Search memory for the sequence of bytes specified by `val1` inclusive.

`s` are optional parameters. They may be specified in either order, apart or together.

[`s`

:   The size of each search query value.

```
`b`

:   bytes

`h`

:   halfwords (two bytes)

`w`

:   words (four bytes)

`g`

:   giant words (eight bytes)

All values are interpreted in the current language. This means, for example, that if the current source language is C/C++ then searching for the string "hello" includes the trailing '\\0'. The null terminator can be removed from searching by using casts, e.g.: '`'.

If the value size is not specified, it is taken from the value's type in the current language. This is useful when one wants to specify the search pattern as a mixture of types. Note that this means, for example, that in the case of C-like languages a search for an untyped 0x42 will search for '`(int) 0x42`' which is typically four bytes.
```

[`n`


:   The maximum number of matches to print. The default is to print all finds.

> 最多打印的匹配数。默认是打印所有的发现。


You can use strings as search values. Quote them with double-quotes (`"`). The string value is copied into the search pattern byte by byte, regardless of the endianness of the target and the size specification.

> 你可以使用字符串作为搜索值。用双引号（`"`）引用它们。无论目标的大小端和大小规格如何，字符串值都会被一个字节一个字节地复制到搜索模式中。


The address of each match found is printed as well as a count of the number of matches found.

> 每个匹配到的地址都会被打印出来，同时也会显示出找到的匹配数量。


The address of the last value found is stored in convenience variable '`$_`'.

> 在便利變量'$_'中存儲最後找到的值的地址。

For example, if stopped at the `printf` in this function:

::: smallexample

```bash
void
hello ()
{
  static char hello = "hello-hello";
  static struct 
    __attribute__ ((packed)) mixed
    = ;
  printf ("%s\n", hello);
}
```

:::

you get during debugging:

::: smallexample

```bash
(gdb) find &hello[0], +sizeof(hello), "hello"
0x804956d <hello.1620+6>
1 pattern found
(gdb) find &hello[0], +sizeof(hello), 'h', 'e', 'l', 'l', 'o'
0x8049567 <hello.1620>
0x804956d <hello.1620+6>
2 patterns found.
(gdb) find &hello[0], +sizeof(hello), "hello"
0x8049567 <hello.1620>
0x804956d <hello.1620+6>
2 patterns found.
(gdb) find /b1 &hello[0], +sizeof(hello), 'h', 0x65, 'l'
0x8049567 <hello.1620>
1 pattern found
(gdb) find &mixed, +sizeof(mixed), (char) 'c', (short) 0x1234, (int) 0x87654321
0x8049560 <mixed.1625>
1 pattern found
(gdb) print $numfound
$1 = 1
(gdb) print $_
$2 = (void *) 0x8049560
```

:::

---

::: header
Next: [Value Sizes](Value-Sizes.html#Value-Sizes)]
:::
