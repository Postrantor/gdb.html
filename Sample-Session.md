---
tip: translate by openai@2023-06-24 02:16:27
...
---
description: Sample Session (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Sample Session (Debugging with GDB)
lang: en
resource-type: document
title: Sample Session (Debugging with GDB)
---
::: header
Next: [Invocation](Invocation.html#Invocation)]
:::

---

## 1 A Sample [GDB]


You can use this manual at your leisure to read all about [GDB]. However, a handful of commands are enough to get started using the debugger. This chapter illustrates those commands.

> 您可以在闲暇时使用本手册阅读有关[GDB]的所有内容。但是，只需要几个命令就可以开始使用调试器。本章介绍了这些命令。


One of the preliminary versions of [GNU] `m4` (a generic macro processor) exhibits the following bug: sometimes, when we change its quote strings from the default, the commands used to capture one macro definition within another stop working. In the following short `m4` session, we define a macro `foo` which expands to `0000`; we then use the `m4` built-in `defn` to define `bar` as the same thing. However, when we change the open quote string to `<QUOTE>` and the close quote string to `<UNQUOTE>`, the same procedure fails to define a new synonym `baz`:

> 一个GNU 'm4（一个通用宏处理器）的初步版本存在以下错误：有时，当我们将其引号字符串从默认值更改时，用于在另一个宏定义中捕获一个宏定义的命令停止工作。在以下简短的`m4`会话中，我们定义了一个宏`foo`，该宏展开为`0000`；然后，我们使用`m4`内置的`defn`来将`bar`定义为相同的东西。但是，当我们将开放引号字符串更改为`<QUOTE>`，并将关闭引号字符串更改为`<UNQUOTE>`时，相同的过程无法定义新的同义词`baz`：

::: smallexample

```bash
$ cd gnu/m4
$ ./m4
define(foo,0000)

foo
0000
define(bar,defn(‘foo’))

bar
0000
changequote(<QUOTE>,<UNQUOTE>)

define(baz,defn(<QUOTE>foo<UNQUOTE>))
baz
Ctrl-d
m4: End of input: 0: fatal error: EOF in string
```

:::

Let us use [GDB] to try to see what is going on.

::: smallexample

```bash
$ gdb m4
GDB is free software and you are welcome to distribute copies
 of it under certain conditions; type "show copying" to see
 the conditions.
There is absolutely no warranty for GDB; type "show warranty"
 for details.

GDB 14.0.50.20230622-git, Copyright 1999 Free Software Foundation, Inc...
(gdb)
```

:::


[GDB] to use a narrower display width than usual, so that examples fit in this manual.

> 使用比通常更窄的显示宽度，以便示例适合本手册。

::: smallexample

```bash
(gdb) set width 70
```

:::


We need to see how the `m4` built-in `changequote` works. Having looked at the source, we know the relevant subroutine is `m4_changequote`, so we set a breakpoint there with the [GDB] `break` command.

> 我们需要看看内置的`m4`的`changequote`是如何工作的。经过查看源代码，我们知道相关的子程序是`m4_changequote`，因此我们使用[GDB]的`break`命令在那里设置断点。

::: smallexample

```bash
(gdb) break m4_changequote
Breakpoint 1 at 0x62f4: file builtin.c, line 879.
```

:::


Using the `run` command, we start `m4` running under [GDB] control; as long as control does not reach the `m4_changequote` subroutine, the program runs as usual:

> 使用`run`命令，我们可以在GDB控制下启动`m4`；只要控制不到达`m4_changequote`子程序，程序就会正常运行：

::: smallexample

```bash
(gdb) run
Starting program: /work/Editorial/gdb/gnu/m4/m4
define(foo,0000)

foo
0000
```

:::


To trigger the breakpoint, we call `changequote`. [GDB] suspends execution of `m4`, displaying information about the context where it stops.

> 要触发断点，我们调用`changequote`。[GDB]暂停了`m4`的执行，显示有关其停止位置的上下文信息。

::: smallexample

```bash
changequote(<QUOTE>,<UNQUOTE>)

Breakpoint 1, m4_changequote (argc=3, argv=0x33c70)
    at builtin.c:879
879         if (bad_argc(TOKEN_DATA_TEXT(argv[0]),argc,1,3))
```

:::


Now we use the command `n` (`next`) to advance execution to the next line of the current function.

> 现在我们使用命令`n`（`next`）来将执行推进到当前函数的下一行。

::: smallexample

```bash
(gdb) n
882         set_quotes((argc >= 2) ? TOKEN_DATA_TEXT(argv[1])\
 : nil,
```

:::

`set_quotes` looks like a promising subroutine. We can go into it by using the command `s` (`step`) instead of `next`. `step` goes to the next line to be executed in *any* subroutine, so it steps into `set_quotes`.

::: smallexample

```bash
(gdb) s
set_quotes (lq=0x34c78 "<QUOTE>", rq=0x34c88 "<UNQUOTE>")
    at input.c:530
530         if (lquote != def_lquote)
```

:::


The display that shows the subroutine where `m4` is now suspended (and its arguments) is called a stack frame display. It shows a summary of the stack. We can use the `backtrace` command (which can also be spelled `bt`), to see where we are in the stack as a whole: the `backtrace` command displays a stack frame for each active subroutine.

> 显示当前`m4`挂起的子程序及其参数的展示叫做堆栈帧显示。它显示了堆栈的概要。我们可以使用`backtrace`命令（也可以拼写为`bt`）来查看整个堆栈中的位置：`backtrace`命令会为每个活动子程序显示一个堆栈帧。

::: smallexample

```bash
(gdb) bt
#0  set_quotes (lq=0x34c78 "<QUOTE>", rq=0x34c88 "<UNQUOTE>")
    at input.c:530
#1  0x6344 in m4_changequote (argc=3, argv=0x33c70)
    at builtin.c:882
#2  0x8174 in expand_macro (sym=0x33320) at macro.c:242
#3  0x7a88 in expand_token (obs=0x0, t=209696, td=0xf7fffa30)
    at macro.c:71
#4  0x79dc in expand_input () at macro.c:40
#5  0x2930 in main (argc=0, argv=0xf7fffb20) at m4.c:195
```

:::


We step through a few more lines to see what happens. The first two times, we can use '`s`'; the next two times we use `n` to avoid falling into the `xstrdup` subroutine.

> 我们再走几行看看会发生什么。前两次，我们可以使用“s”；接下来两次我们使用“n”来避免跌入`xstrdup`子程序。

::: smallexample

```bash
(gdb) s
0x3b5c  532         if (rquote != def_rquote)
(gdb) s
0x3b80  535         lquote = (lq == nil || *lq == '\0') ?  \
def_lquote : xstrdup(lq);
(gdb) n
536         rquote = (rq == nil || *rq == '\0') ? def_rquote\
 : xstrdup(rq);
(gdb) n
538         len_lquote = strlen(rquote);
```

:::


The last line displayed looks a little odd; we can examine the variables `lquote` and `rquote` to see if they are in fact the new left and right quotes we specified. We use the command `p` (`print`) to see their values.

> 最后一行显示的看起来有点奇怪；我们可以检查变量`lquote`和`rquote`，看它们是否实际上是我们指定的新的左右引号。我们使用命令`p`（`print`）来查看它们的值。

::: smallexample

```bash
(gdb) p lquote
$1 = 0x35d40 "<QUOTE>"
(gdb) p rquote
$2 = 0x35d50 "<UNQUOTE>"
```

:::

`lquote` and `rquote` are indeed the new left and right quotes. To look at some context, we can display ten lines of source surrounding the current line with the `l` (`list`) command.

::: smallexample

```bash
(gdb) l
533             xfree(rquote);
534
535         lquote = (lq == nil || *lq == '\0') ? def_lquote\
 : xstrdup (lq);
536         rquote = (rq == nil || *rq == '\0') ? def_rquote\
 : xstrdup (rq);
537
538         len_lquote = strlen(rquote);
539         len_rquote = strlen(lquote);
540     }
541
542     void
```

:::


Let us step past the two lines that set `len_lquote` and `len_rquote`, and then examine the values of those variables.

> 让我们跳过设置`len_lquote`和`len_rquote`的两条线，然后检查这些变量的值。

::: smallexample

```bash
(gdb) n
539         len_rquote = strlen(lquote);
(gdb) n
540     }
(gdb) p len_lquote
$3 = 9
(gdb) p len_rquote
$4 = 7
```

:::


That certainly looks wrong, assuming `len_lquote` and `len_rquote` are meant to be the lengths of `lquote` and `rquote` respectively. We can set them to better values using the `p` command, since it can print the value of any expression---and that expression can include subroutine calls and assignments.

> 那看起来肯定不对，假设`len_lquote`和`len_rquote`分别是`lquote`和`rquote`的长度。我们可以使用`p`命令将它们设置为更好的值，因为它可以打印任何表达式的值---而这个表达式可以包括子程序调用和赋值。

::: smallexample

```bash
(gdb) p len_lquote=strlen(lquote)
$5 = 7
(gdb) p len_rquote=strlen(rquote)
$6 = 9
```

:::


Is that enough to fix the problem of using the new quotes with the `m4` built-in `defn`? We can allow `m4` to continue executing with the `c` (`continue`) command, and then try the example that caused trouble initially:

> 这足以解决使用新引号和m4内置defn的问题吗？我们可以允许m4继续使用c（continue）命令执行，然后尝试最初引起麻烦的示例：

::: smallexample

```bash
(gdb) c
Continuing.

define(baz,defn(<QUOTE>foo<UNQUOTE>))

baz
0000
```

:::


Success! The new quotes now work just as well as the default ones. The problem seems to have been just the two typos defining the wrong lengths. We allow `m4` exit by giving it an EOF as input:

> 成功！新的引用现在和默认的一样有效。问题似乎只是定义错误长度的两个拼写错误。我们通过给它输入EOF来允许`m4`退出：

::: smallexample

```bash
Ctrl-d
Program exited normally.
```

:::

The message '`Program exited normally.` `quit` command.

::: smallexample

```bash
(gdb) quit
```

:::

---

::: header
Next: [Invocation](Invocation.html#Invocation)]
:::
