---
tip: translate by openai@2023-06-23 13:20:01
...
---
description: Skipping Over Functions and Files (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Skipping Over Functions and Files (Debugging with GDB)
lang: en
resource-type: document
title: Skipping Over Functions and Files (Debugging with GDB)
-------------------------------------------------------------

::: header
Next: [Signals](Signals.html#Signals)]
:::

---

### 5.3 Skipping Over Functions and Files

The program you are debugging may contain some functions which are uninteresting to debug. The `skip` command lets you tell [GDB] to skip a function, all functions in a file or a particular function in a particular file when stepping.

> 你正在调试的程序可能包含一些无趣的函数。`skip` 命令可以让你告诉[GDB]在调试时跳过一个函数、一个文件中的所有函数或特定文件中的特定函数。

For example, consider the following C function:

> 例如，考虑下面的 C 函数：

::: smallexample

```bash
101     int func()
102     {
103         foo(boring());
104         bar(boring());
105     }
```

:::

Suppose you wish to step into the functions `foo` and `bar`, but you are not interested in stepping through `boring`. If you run `step` at line 103, you'll enter `boring()`, but if you run `next`, you'll step over both `foo` and `boring`!

> 如果你想进入函数 `foo` 和 `bar`，但不想调试 `boring`，那么如果你在第 103 行运行 `step`，你将进入 `boring()`，但如果你运行 `next`，你将跳过 `foo` 和 `boring`！

One solution is to `step` into `boring` and use the `finish` command to immediately exit it. But this can become tedious if `boring` is called from many places.

> 一个解决方案是进入 `boring` 并使用 `finish` 命令立即退出。但是，如果 `boring` 从许多地方调用，这可能变得很繁琐。

A more flexible solution is to execute [skip boring] never to step into `boring`. Now when you execute `step` at line 103, you'll step over `boring` and directly into `foo`.

> 一个更灵活的解决方案是执行[跳过无聊]永远不会踏入“无聊”。现在，当您在第 103 行执行“步骤”时，您将跳过“无聊”并直接进入“foo”。

Functions may be skipped by providing either a function name, linespec (see [Location Specifications](Location-Specifications.html#Location-Specifications)), regular expression that matches the function's name, file name or a `glob`-style pattern that matches the file name.

> 函数可以通过提供函数名、行号（参见[位置规范](Location-Specifications.html#Location-Specifications))、匹配函数名的正则表达式、文件名或匹配文件名的 `glob` 样式模式来跳过。

On Posix systems the form of the regular expression is "Extended Regular Expressions". See for example '`man 7 regex`/Linux systems for a description of `glob`-style patterns.

> 在 POSIX 系统中，正则表达式的格式为“扩展正则表达式”。例如，参见'man 7 regex' / Linux 系统，了解 glob 样式模式的描述。

`skip [options]`

The basic form of the `skip` command takes zero or more options that specify what to skip. The `options` argument is any useful combination of the following:

> 基本形式的 `skip` 命令接受零个或多个选项，用于指定跳过什么。`选项` 参数是以下任何有用组合：

`-file file`
`-fi file`

:   Functions in `file` will be skipped over when stepping.

> 函数在 `文件` 中将被跳过，而不被步进。

`-gfile file-glob-pattern`
`-gfi file-glob-pattern`

:

```
Functions in files matching `file-glob-pattern` will be skipped over when stepping.

::: smallexample
``` smallexample

(gdb) skip -gfi utils/*.c

> (gdb) 跳过 -gfi utils/*.c
```

:::

```

`-function linespec`
`-fu linespec`


:   Functions named by `linespec` will be skipped over when stepping. See [Location Specifications](Location-Specifications.html#Location-Specifications).

> 函数命名为`linespec`时，在跳过时会被忽略。请参阅[位置规范](Location-Specifications.html#Location-Specifications)。

`-rfunction regexp`
`-rfu regexp`

:   

```

Functions whose name matches `regexp` will be skipped over when stepping.

This form is useful for complex function names. For example, there is generally no need to step into C++ `std::string` constructors or destructors. Plus with C++ templates it can be hard to write out the full name of the function, and often it doesn't matter what the template arguments are. Specifying the function to be skipped as a regular expression makes this easier.

::: smallexample

```bash

(gdb) skip -rfu ^std::(allocator|basic_string)<.*>::~?\1 *\(

> (gdb) 跳过 -rfu ^std::(allocator|basic_string)<.*>::~?\1 *\(
```

:::

If you want to skip every templated C++ constructor and destructor in the `std` namespace you can do:

::: smallexample

```bash

(gdb) skip -rfu ^std::([a-zA-z0-9_]+)<.*>::~?\1 *\(

> (gdb) 跳过 -rfu ^std::([a-zA-z0-9_]+)<.*>::~?\1 *\(
```

:::

```


If no options are specified, the function you're currently debugging will be skipped.

> 如果没有指定选项，您当前正在调试的函数将被跳过。



`skip function [linespec]`


After running this command, the function named by `linespec` will be skipped over when stepping. See [Location Specifications](Location-Specifications.html#Location-Specifications).

> 在运行此命令之后，名为`linespec`的函数将被跳过，在调试中跳过。请参见[位置规范](Location-Specifications.html#Location-Specifications)。


If you do not specify `linespec`, the function you're currently debugging will be skipped.

> 如果您没有指定`linespec`，您当前正在调试的函数将被跳过。


(If you have a function called `file` that you want to skip, use [skip function file].)

> 如果你有一个叫做`file`的函数你想要跳过，使用[跳过函数file]。



`skip file [filename]`


After running this command, any function whose source lives in `filename` will be skipped over when stepping.

> 在运行此命令之后，任何源代码位于`filename`中的函数将被跳过。

::: smallexample

```bash
(gdb) skip file boring.c
File boring.c will be skipped when stepping.
```

:::

If you do not specify `filename`, functions whose source lives in the file you're currently debugging will be skipped.

> 如果您不指定“文件名”，那么源代码位于当前调试文件中的函数将被跳过。

Skips can be listed, deleted, disabled, and enabled, much like breakpoints. These are the commands for managing your list of skips:

> 跳过可以像断点一样被列出、删除、禁用和启用。以下是管理跳过列表的命令：

`info skip [range]`

Print details about the specified skip(s). If `range` is not specified, print a table with details about all functions and files marked for skipping. `info skip` prints the following information about each skip:

> 打印关于指定跳过的详细信息。如果未指定“范围”，则打印一个表，其中包含有关标记为跳过的所有函数和文件的详细信息。“info skip”会打印每个跳过的以下信息：

*Identifier*

:   A number identifying this skip.

> 这个跳跃的标识号。

*Enabled or Disabled*

:   Enabled skips are marked with '`y`'.

> 跳过的已启用项标记为'`y`'。

*Glob*

:   If the file name is a '`glob`'.

> 如果文件名是一个'`glob`'。

*File*

:   The name or '`glob`'.

> 全局名称或“glob”。

*RE*

:   If the function name is a '`regular expression`'.

> 如果函数名是一个"正则表达式"

*Function*

:   The name or regular expression of the function to skip. If no function is specified this is '`<none>`'.

> 此功能的名称或正则表达式以跳过。如果未指定任何函数，则为“<none>”。

`skip delete [range]`

Delete the specified skip(s). If `range` is not specified, delete all skips.

> 删除指定的跳过项（如果未指定范围，则删除所有跳过项）。

`skip enable [range]`

Enable the specified skip(s). If `range` is not specified, enable all skips.

> 启用指定的跳过（s）。如果未指定 `范围`，则启用所有跳过。

`skip disable [range]`

Disable the specified skip(s). If `range` is not specified, disable all skips.

> 禁用指定的跳过(s)。如果未指定 `范围`，则禁用所有跳过。

`set debug skip [on|off]`

Set whether to print the debug output about skipping files and functions.

> 设置是否打印有关跳过文件和函数的调试输出。

`show debug skip`

Show whether the debug output about skipping files and functions is printed.

> 检查调试输出是否打印有关跳过文件和函数的信息。

---

::: header
Next: [Signals](Signals.html#Signals)]
:::
