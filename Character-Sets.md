---
tip: translate by openai@2023-06-23 18:52:01
...
---
description: Character Sets (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Character Sets (Debugging with GDB)
lang: en
resource-type: document
title: Character Sets (Debugging with GDB)
---
::: header
Next: [Caching Target Data](Caching-Target-Data.html#Caching-Target-Data)]
:::

---

### 10.21 Character Sets


If the program you are debugging uses a different character set to represent characters and strings than the one [GDB] uses we call the *host character set*; the one the inferior program uses we call the *target character set*.

> 如果正在调试的程序使用与[GDB]不同的字符集来表示字符和字符串，我们称之为*主机字符集*；被调试程序使用的称为*目标字符集*。


For example, if you are running [GDB] and Latin 1 as you print character or string values, or use character and string literals in expressions.

> 例如，如果您正在运行[GDB]并使用Latin 1打印字符或字符串值，或在表达式中使用字符和字符串文字。


[GDB] has no way to automatically recognize which character set the inferior program uses; you must tell it, using the `set target-charset` command, described below.

> GDB没有办法自动识别下层程序使用的字符集；您必须使用下文描述的`set target-charset`命令来告诉它。


Here are the commands for controlling [GDB]'s character set support:

> 以下是控制GDB字符集支持的命令：

`set target-charset charset`

:

```
Set the current target character set to `charset`.
```

`set host-charset charset`

:

```
Set the current host character set to `charset`.

By default, [GDB]'.

[GDB] will list the host character sets it supports.
```

`set charset charset`

:

```
Set the current host and target character sets to `charset` will list the names of the character sets that can be used for both host and target.
```

`show charset`

:

```
Show the names of the current host and target character sets.
```

`show host-charset`

:

```
Show the name of the current host character set.
```

`show target-charset`

:

```
Show the name of the current target character set.
```

`set target-wide-charset charset`

:

```
Set the current target's wide character set to `charset`.
```

`show target-wide-charset`

:

```
Show the name of the current target's wide character set.
```


Here is an example of [GDB]:

> 这里是一个GDB的例子：

::: smallexample

```bash
#include <stdio.h>

char ascii_hello
  = {72, 101, 108, 108, 111, 44, 32, 119,
     111, 114, 108, 100, 33, 10, 0};
char ibm1047_hello
  = {200, 133, 147, 147, 150, 107, 64, 166,
     150, 153, 147, 132, 90, 37, 0};

main ()
{
  printf ("Hello, world!\n");
}
```

:::


In this program, `ascii_hello` and `ibm1047_hello` are arrays containing the string '`Hello, world!` character sets.

> 在这个程序中，`ascii_hello`和`ibm1047_hello`都是包含字符串'`Hello, world!`字符集的数组。


We compile the program, and invoke the debugger on it:

> 我们编译程序，并在其上调用调试器：

::: smallexample

```bash
$ gcc -g charset-test.c -o charset-test
$ gdb -nw charset-test
GNU gdb 2001-12-19-cvs
Copyright 2001 Free Software Foundation, Inc.
…
(gdb)
```

:::


We can use the `show charset` command to see what character sets [GDB] is currently using to interpret and display characters and strings:

> 我们可以使用`show charset`命令来查看[GDB]当前用于解释和显示字符和字符串的字符集：

::: smallexample

```bash
(gdb) show charset
The current host and target character set is `ISO-8859-1'.
(gdb)
```

:::


For the sake of printing this manual, let's use [ASCII] as our initial character set:

> 为了打印本手册，让我们以[ASCII]作为初始字符集：

::: smallexample

```bash
(gdb) set charset ASCII
(gdb) show charset
The current host and target character set is `ASCII'.
(gdb)
```

:::


Let's assume that [ASCII], the contents of `ascii_hello` print legibly:

> 让我们假设[ASCII]，`ascii_hello`的内容可以清晰地打印出来。

::: smallexample

```bash
(gdb) print ascii_hello
$1 = 0x401698 "Hello, world!\n"
(gdb) print ascii_hello[0]
$2 = 72 'H'
(gdb)
```

:::


[GDB] uses the target character set for character and string literals you use in expressions:

> [GDB] 使用目标字符集来处理表达式中使用的字符和字符串字面量。

::: smallexample

```bash
(gdb) print '+'
$3 = 43 '+'
(gdb)
```

:::

The [ASCII]' character.


[GDB], we get jibberish:

> 我们得到了胡言乱语：[GDB]

::: smallexample

```bash
(gdb) print ibm1047_hello
$4 = 0x4016a8 "\310\205\223\223\226k@\246\226\231\223\204Z%"
(gdb) print ibm1047_hello[0]
$5 = 200 '\310'
(gdb)
```

:::


If we invoke the `set target-charset` followed by TABTAB, [GDB] tells us the character sets it supports:

> 如果我们调用`set target-charset`后跟TABTAB，[GDB]会告诉我们它支持的字符集：简体中文

::: smallexample

```bash
(gdb) set target-charset
ASCII       EBCDIC-US   IBM1047     ISO-8859-1
(gdb) set target-charset
```

:::


We can select [IBM1047], and they display correctly:

> 我们可以选择[IBM1047]，它们会正确显示。

::: smallexample

```bash
(gdb) set target-charset IBM1047
(gdb) show charset
The current host character set is `ASCII'.
The current target character set is `IBM1047'.
(gdb) print ascii_hello
$6 = 0x401698 "\110\145%%?\054\040\167?\162%\144\041\012"
(gdb) print ascii_hello[0]
$7 = 72 '\110'
(gdb) print ibm1047_hello
$8 = 0x4016a8 "Hello, world!\n"
(gdb) print ibm1047_hello[0]
$9 = 200 'H'
(gdb)
```

:::


As above, [GDB] uses the target character set for character and string literals you use in expressions:

> 如上所述，[GDB]使用目标字符集来表示您在表达式中使用的字符和字符串文字。

::: smallexample

```bash
(gdb) print '+'
$10 = 78 '+'
(gdb)
```

:::


The [IBM1047]' character.

> IBM1047字符

---

::: header
Next: [Caching Target Data](Caching-Target-Data.html#Caching-Target-Data)]
:::
