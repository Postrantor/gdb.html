---
tip: translate by openai@2023-06-24 10:34:03
...
---
description: Macros (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Macros (Debugging with GDB)
lang: en
resource-type: document
title: Macros (Debugging with GDB)
---
::: header
Next: [Tracepoints](Tracepoints.html#Tracepoints)]
:::

---

## 12 C Preprocessor Macros


Some languages, such as C and C++, provide a way to define and invoke "preprocessor macros" which expand into strings of tokens. [GDB] can evaluate expressions containing macro invocations, show the result of macro expansion, and show a macro's definition, including where it was defined.

> 一些语言，如C和C++，提供一种方式来定义和调用“预处理器宏”，它们展开为令牌串。[GDB]可以评估包含宏调用的表达式，显示宏展开的结果，并显示宏的定义，包括它定义的位置。


You may need to compile your program specially to provide [GDB] flag. See [Compilation](Compilation.html#Compilation).

> 你可能需要特别编译你的程序来提供[GDB]标志。参见[编译](Compilation.html#Compilation)。


A program may define a macro at one point, remove that definition later, and then provide a different definition after that. Thus, at different points in the program, a macro may have different definitions, or have no definition at all. If there is a current stack frame, [GDB] uses the macros in scope at the current listing location; see [List](List.html#List).

> 一个程序可以在一个点定义一个宏，稍后删除该定义，然后提供另一个定义。因此，在程序的不同点，宏可能具有不同的定义，也可能没有定义。如果有当前堆栈帧，[GDB]将使用当前清单位置范围内的宏；请参见[列表](List.html#List)。


Whenever [GDB] also provides the following commands for working with macros explicitly.

> 每当GDB也提供以下命令来显式地处理宏。

`macro expand expression`

`macro exp expression`


Show the results of expanding all preprocessor macro invocations in `expression` need not be a valid expression; it can be any string of tokens.

> 不需要表达式是有效的，`expression`可以是任意一组标记，展开所有预处理器宏调用的结果就是这样。

`macro expand-once expression`

`macro exp1 expression`


*(This command is not yet implemented.)* Show the results of expanding those preprocessor macro invocations that appear explicitly in `expression` need not be a valid expression; it can be any string of tokens.

> *（此命令尚未实现。）在`expression`中显式出现的预处理器宏调用的结果，不需要是有效表达式；它可以是任何一串令牌。*

`info macro [-a|-all] [--] macro`


Show the current definition or all definitions of the named `macro` for non C-like macros where the macro may begin with a hyphen.

> 显示所命名的“宏”的当前定义或所有定义，对于以连字符开头的非C语言宏。

`info macros locspec`


Show all macro definitions that are in effect at the source line of the code location that results from resolving `locspec`, and describe the source location or compiler command-line where those definitions were established.

> 显示在从解析`locspec`而得到的代码位置处生效的所有宏定义，并描述建立这些定义的源位置或编译器命令行。

`macro define macro replacement-list`

`macro define macro(arglist) replacement-list`

Introduce a definition for a preprocessor macro named `macro`.


A definition introduced by this command is in scope in every expression evaluated in [GDB] present in the program being debugged, as well as any previous user-supplied definition.

> 此命令引入的定义在调试程序中的[GDB]中评估的每个表达式以及任何以前用户提供的定义中均有效。

`macro undef macro`


Remove any user-supplied definition for the macro named `macro`. This command only affects definitions provided with the `macro define` command, described above; it cannot remove definitions present in the program being debugged.

> 删除名为“宏”的任何用户提供的宏定义。此命令仅影响使用“宏定义”命令（如上所述）提供的定义；它不能删除正在调试的程序中存在的定义。

`macro list`

List all the macros defined using the `macro define` command.


Here is a transcript showing the above commands in action. First, we show our source files:

> 这里有一份成绩单，显示了上述命令的操作。首先，我们显示我们的源文件：

::: smallexample

```bash
$ cat sample.c
#include <stdio.h>
#include "sample.h"

#define M 42
#define ADD(x) (M + x)

main ()
{
#define N 28
  printf ("Hello, world!\n");
#undef N
  printf ("We're so creative.\n");
#define N 1729
  printf ("Goodbye, world!\n");
}
$ cat sample.h
#define Q <
$
```

:::


Now, we compile the program using the [GNU] flags to ensure the compiler includes information about preprocessor macros in the debugging information.

> 现在，我们使用[GNU]标志来编译程序，以确保编译器将预处理器宏的信息包括在调试信息中。

::: smallexample

```bash
$ gcc -gdwarf-2 -g3 sample.c -o sample
$
```

:::

Now, we start [GDB] on our sample program:

::: smallexample

```bash
$ gdb -nw sample
GNU gdb 2002-05-06-cvs
Copyright 2002 Free Software Foundation, Inc.
GDB is free software, …
(gdb)
```

:::


We can expand macros and examine their definitions, even when the program is not running. [GDB] uses the current listing position to decide which macro definitions are in scope:

> 我们可以展开宏，甚至在程序未运行时也可以检查它们的定义。[GDB]使用当前列表位置来决定哪些宏定义是有效的。

::: smallexample

```bash
(gdb) list main
3
4       #define M 42
5       #define ADD(x) (M + x)
6
7       main ()
8       {
9       #define N 28
10        printf ("Hello, world!\n");
11      #undef N
12        printf ("We're so creative.\n");
(gdb) info macro ADD
Defined at /home/jimb/gdb/macros/play/sample.c:5
#define ADD(x) (M + x)
(gdb) info macro Q
Defined at /home/jimb/gdb/macros/play/sample.h:1
  included at /home/jimb/gdb/macros/play/sample.c:2
#define Q <
(gdb) macro expand ADD(1)
expands to: (42 + 1)
(gdb) macro expand-once ADD(1)
expands to: once (M + 1)
(gdb)
```

:::


In the example above, note that `macro expand-once` expands only the macro invocation explicit in the original text --- the invocation of `ADD` --- but does not expand the invocation of the macro `M`, which was introduced by `ADD`.

> 在上面的例子中，注意`macro expand-once`只展开原始文本中显式调用的宏---调用`ADD`---但不展开由`ADD`引入的宏`M`的调用。


Once the program is running, [GDB] uses the macro definitions in force at the source line of the current stack frame:

> 一旦程序运行，[GDB]就会使用当前堆栈帧中源代码行的宏定义。

::: smallexample

```bash
(gdb) break main
Breakpoint 1 at 0x8048370: file sample.c, line 10.
(gdb) run
Starting program: /home/jimb/gdb/macros/play/sample

Breakpoint 1, main () at sample.c:10
10        printf ("Hello, world!\n");
(gdb)
```

:::

At line 10, the definition of the macro `N` at line 9 is in force:

::: smallexample

```bash
(gdb) info macro N
Defined at /home/jimb/gdb/macros/play/sample.c:9
#define N 28
(gdb) macro expand N Q M
expands to: 28 < 42
(gdb) print N Q M
$1 = 1
(gdb)
```

:::


As we step over directives that remove `N`'s definition, and then give it a new definition, [GDB] finds the definition (or lack thereof) in force at each point:

> 随着我们跨越删除N的定义的指令，然后给它一个新的定义，GDB在每个点上发现生效的定义（或缺失）。

::: smallexample

```bash
(gdb) next
Hello, world!
12        printf ("We're so creative.\n");
(gdb) info macro N
The symbol `N' has no definition as a C/C++ preprocessor macro
at /home/jimb/gdb/macros/play/sample.c:12
(gdb) next
We're so creative.
14        printf ("Goodbye, world!\n");
(gdb) info macro N
Defined at /home/jimb/gdb/macros/play/sample.c:13
#define N 1729
(gdb) macro expand N Q M
expands to: 1729 < 42
(gdb) print N Q M
$2 = 0
(gdb)
```

:::


In addition to source files, macros can be defined on the compilation command line using the `-Dname=value` displays the location of their definition as line zero of the source file submitted to the compiler.

> 除源文件外，可以使用`-Dname=value`在编译命令行上定义宏，它将其定义的位置显示为提交给编译器的源文件的零行。

::: smallexample

```bash
(gdb) info macro __STDC__
Defined at /home/jimb/gdb/macros/play/sample.c:0
-D__STDC__=1
(gdb)
```

:::

::: footnote

---

#### Footnotes

### [(14)](#DOCF14)


This is the minimum. Recent versions of [GCC]; we recommend always choosing the most recent version of DWARF.

> 这是最低要求。我们建议总是选择最新版本的DWARF，最近版本的GCC。
:::

---

::: header
Next: [Tracepoints](Tracepoints.html#Tracepoints)]
:::
