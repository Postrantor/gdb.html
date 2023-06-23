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

You may need to compile your program specially to provide [GDB] flag. See [Compilation](Compilation.html#Compilation).

A program may define a macro at one point, remove that definition later, and then provide a different definition after that. Thus, at different points in the program, a macro may have different definitions, or have no definition at all. If there is a current stack frame, [GDB] uses the macros in scope at the current listing location; see [List](List.html#List).

Whenever [GDB] also provides the following commands for working with macros explicitly.

`macro expand expression`

`macro exp expression`

Show the results of expanding all preprocessor macro invocations in `expression` need not be a valid expression; it can be any string of tokens.

`macro expand-once expression`

`macro exp1 expression`

*(This command is not yet implemented.)* Show the results of expanding those preprocessor macro invocations that appear explicitly in `expression` need not be a valid expression; it can be any string of tokens.

`info macro [-a|-all] [--] macro`

Show the current definition or all definitions of the named `macro` for non C-like macros where the macro may begin with a hyphen.

`info macros locspec`

Show all macro definitions that are in effect at the source line of the code location that results from resolving `locspec`, and describe the source location or compiler command-line where those definitions were established.

`macro define macro replacement-list`

`macro define macro(arglist) replacement-list`

Introduce a definition for a preprocessor macro named `macro`.

A definition introduced by this command is in scope in every expression evaluated in [GDB] present in the program being debugged, as well as any previous user-supplied definition.

`macro undef macro`

Remove any user-supplied definition for the macro named `macro`. This command only affects definitions provided with the `macro define` command, described above; it cannot remove definitions present in the program being debugged.

`macro list`

List all the macros defined using the `macro define` command.

Here is a transcript showing the above commands in action. First, we show our source files:

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

Once the program is running, [GDB] uses the macro definitions in force at the source line of the current stack frame:

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
:::

---

::: header
Next: [Tracepoints](Tracepoints.html#Tracepoints)]
:::
