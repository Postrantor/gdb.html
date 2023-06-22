---
description: Assignment (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Assignment (Debugging with GDB)
lang: en
resource-type: document
title: Assignment (Debugging with GDB)
---
::: header
Next: [Jumping](Jumping.html#Jumping)]
:::

---

### 17.1 Assignment to Variables

To alter the value of a variable, evaluate an assignment expression. See [Expressions](Expressions.html#Expressions). For example,

::: smallexample

```bash
print x=4
```

:::

stores the value 4 into the variable `x`, and then prints the value of the assignment expression (which is 4). See [Using [GDB] with Different Languages](Languages.html#Languages), for more information on operators in supported languages.

If you are not interested in seeing the value of the assignment, use the `set` command instead of the `print` command. `set` is really the same as `print` except that the expression's value is not printed and is not put in the value history (see [Value History](Value-History.html#Value-History)). The expression is evaluated only for its effects.

If the beginning of the argument string of the `set` command appears identical to a `set` subcommand, use the `set variable` command instead of just `set`. This command is identical to `set` except for its lack of subcommands. For example, if your program has a variable `width`, you get an error if you try to set a new value with just '`set width=13` has the command `set width`:

::: smallexample

```bash
(gdb) whatis width
type = double
(gdb) p width
$4 = 13
(gdb) set width=47
Invalid syntax in expression.
```

:::

The invalid expression, of course, is '`=47`'. In order to actually set the program's variable `width`, use

::: smallexample

```bash
(gdb) set var width=47
```

:::

Because the `set` command has many subcommands that can conflict with the names of program variables, it is a good idea to use the `set variable` command instead of just `set`. For example, if your program has a variable `g`, you run into problems if you try to set a new value with just '`set g=4` has the command `set gnutarget`, abbreviated `set g`:

::: smallexample

```bash
(gdb) whatis g
type = double
(gdb) p g
$1 = 1
(gdb) set g=4
(gdb) p g
$2 = 1
(gdb) r
The program being debugged has been started already.
Start it from the beginning? (y or n) y
Starting program: /home/smith/cc_progs/a.out
"/home/smith/cc_progs/a.out": can't open to read symbols:
                                 Invalid bfd target.
(gdb) show g
The current BFD target is "=4".
```

:::

The program variable `g` did not change, and you silently set the `gnutarget` to an invalid value. In order to set the variable `g`, use

::: smallexample

```bash
(gdb) set var g=4
```

:::

[GDB] allows more implicit conversions in assignments than C; you can freely store an integer value into a pointer variable or vice versa, and you can convert any structure to any other structure that is the same length or shorter.

To store values into arbitrary places in memory, use the '`0x83040` refers to memory location `0x83040` as an integer (which implies a certain size and representation in memory), and

::: smallexample

```bash
set 0x83040 = 4
```

:::

stores the value 4 into that memory location.

---

::: header
Next: [Jumping](Jumping.html#Jumping)]
:::
