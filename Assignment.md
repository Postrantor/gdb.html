---
tip: translate by openai@2023-06-23 17:36:04
...
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

> 要改变变量的值，请评估赋值表达式。请参见[表达式](Expressions.html#Expressions)。例如，

::: smallexample

```bash
print x=4
```

:::


stores the value 4 into the variable `x`, and then prints the value of the assignment expression (which is 4). See [Using [GDB] with Different Languages](Languages.html#Languages), for more information on operators in supported languages.

> 将值4存储到变量x中，然后打印赋值表达式的值（即4）。有关支持语言中的操作符的更多信息，请参阅[使用[GDB]与不同语言]（Languages.html#Languages）。


If you are not interested in seeing the value of the assignment, use the `set` command instead of the `print` command. `set` is really the same as `print` except that the expression's value is not printed and is not put in the value history (see [Value History](Value-History.html#Value-History)). The expression is evaluated only for its effects.

> 如果你不想看到作业的值，请使用`set`命令而不是`print`命令。`set`与`print`实际上是一样的，只是表达式的值不会被打印出来，也不会放入值历史记录中（参见[值历史记录](Value-History.html#Value-History)）。表达式仅仅会被评估其影响。


If the beginning of the argument string of the `set` command appears identical to a `set` subcommand, use the `set variable` command instead of just `set`. This command is identical to `set` except for its lack of subcommands. For example, if your program has a variable `width`, you get an error if you try to set a new value with just '`set width=13` has the command `set width`:

> 如果`set`命令的参数字符串的开头与`set`子命令相同，请使用`set variable`命令而不是仅使用`set`。此命令与`set`除了缺少子命令外完全相同。例如，如果您的程序具有变量`width`，则尝试仅使用“set width = 13”设置新值时会出现错误：命令`set width`：

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

> 无效的表达当然是 '`=47`'。要实际设置程序的变量 `width`，请使用`

::: smallexample

```bash
(gdb) set var width=47
```

:::


Because the `set` command has many subcommands that can conflict with the names of program variables, it is a good idea to use the `set variable` command instead of just `set`. For example, if your program has a variable `g`, you run into problems if you try to set a new value with just '`set g=4` has the command `set gnutarget`, abbreviated `set g`:

> 因为`set`命令有许多子命令可能与程序变量的名称发生冲突，因此最好使用`set variable`命令而不是`set`。例如，如果您的程序有一个变量`g`，如果您尝试使用“set g = 4”设置新值，则会遇到问题：命令`set gnutarget`（简称`set g`）。

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

> 程序变量`g`没有改变，你悄悄地将`gnutarget`设置为了一个无效的值。要设置变量`g`，请使用

::: smallexample

```bash
(gdb) set var g=4
```

:::


[GDB] allows more implicit conversions in assignments than C; you can freely store an integer value into a pointer variable or vice versa, and you can convert any structure to any other structure that is the same length or shorter.

> GDB允许在赋值中更多的隐式转换，比C更宽松；你可以自由地将整数值存储到指针变量中，或者反之亦然，并且你可以将任何结构转换为长度相同或更短的任何其他结构。


To store values into arbitrary places in memory, use the '`0x83040` refers to memory location `0x83040` as an integer (which implies a certain size and representation in memory), and

> 将值存储到内存中任意的位置，使用'0x83040'指代内存位置0x83040，作为一个整数（这意味着在内存中有一定的大小和表示）。

::: smallexample

```bash
set 0x83040 = 4
```

:::


stores the value 4 into that memory location.

> 将值4存储到该内存位置。

---

::: header
Next: [Jumping](Jumping.html#Jumping)]
:::
