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

For example, if you are running [GDB] and Latin 1 as you print character or string values, or use character and string literals in expressions.

[GDB] has no way to automatically recognize which character set the inferior program uses; you must tell it, using the `set target-charset` command, described below.

Here are the commands for controlling [GDB]'s character set support:

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

We compile the program, and invoke the debugger on it:

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

::: smallexample

```bash
(gdb) show charset
The current host and target character set is `ISO-8859-1'.
(gdb)
```

:::

For the sake of printing this manual, let's use [ASCII] as our initial character set:

::: smallexample

```bash
(gdb) set charset ASCII
(gdb) show charset
The current host and target character set is `ASCII'.
(gdb)
```

:::

Let's assume that [ASCII], the contents of `ascii_hello` print legibly:

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

::: smallexample

```bash
(gdb) print '+'
$3 = 43 '+'
(gdb)
```

:::

The [ASCII]' character.

[GDB], we get jibberish:

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

::: smallexample

```bash
(gdb) set target-charset
ASCII       EBCDIC-US   IBM1047     ISO-8859-1
(gdb) set target-charset
```

:::

We can select [IBM1047], and they display correctly:

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

::: smallexample

```bash
(gdb) print '+'
$10 = 78 '+'
(gdb)
```

:::

The [IBM1047]' character.

---

::: header
Next: [Caching Target Data](Caching-Target-Data.html#Caching-Target-Data)]
:::
