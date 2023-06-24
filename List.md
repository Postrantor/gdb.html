---
tip: translate by openai@2023-06-23 23:53:13
...
---
description: List (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: List (Debugging with GDB)
lang: en
resource-type: document
title: List (Debugging with GDB)
---
::: header
Next: [Location Specifications](Location-Specifications.html#Location-Specifications)]
:::

---

### 9.1 Printing Source Lines


To print lines from a source file, use the `list` command (abbreviated `l`). By default, ten lines are printed. There are several ways to specify what part of the file you want to print; see [Location Specifications](Location-Specifications.html#Location-Specifications), for the full list.

> 要打印来自源文件的行，请使用`list`命令（缩写为`l`）。默认情况下，会打印出十行。有几种方法可以指定要打印的文件的哪一部分；有关完整列表，请参见[位置规范](Location-Specifications.html#Location-Specifications)。

Here are the forms of the `list` command most commonly used:

`list linenum`


:   Print lines centered around line number `linenum` in the current source file.

> 打印当前源文件中以行号`linenum`为中心的行。

`list function`

:   Print lines centered around the beginning of function `function`.

`list`


:   Print more lines. If the last lines printed were printed with a `list` command, this prints lines following the last lines printed; however, if the last line printed was a solitary line printed as part of displaying a stack frame (see [Examining the Stack](Stack.html#Stack)), this prints lines centered around that line.

> 打印更多行。如果最后一行是用`list`命令打印的，那么这会打印最后一行之后的行；但是，如果最后一行是作为显示堆栈帧的一部分单独打印的（参见[检查堆栈](Stack.html#Stack)），那么这会打印围绕该行的行。

`list -`

:   Print lines just before the lines last printed.


By default, [GDB] prints ten source lines with any of these forms of the `list` command. You can change this using `set listsize`:

> 默认情况下，使用`list`命令的任何形式，[GDB]都会打印十行源代码。您可以使用`set listsize`来更改此设置。

`set listsize count`

`set listsize unlimited`


Make the `list` command display `count` to `unlimited` or 0 means there's no limit.

> 使用`list`命令显示`count`参数设置为无限或0，表示没有限制。

`show listsize`

Display the number of lines that `list` prints.


Repeating a `list` command with RET discards the argument, so it is equivalent to typing just `list`. This is more useful than listing the same lines again. An exception is made for an argument of '`-`'; that argument is preserved in repetition so that each repetition moves up in the source file.

> 重复输入`list`命令会抛弃参数，因此相当于只输入`list`。这比再次列出相同行更有用。对于参数'`-`'除外；该参数在重复中保留，以便每次重复都在源文件中上移。


In general, the `list` command expects you to supply zero, one or two location specs. These location specs are interpreted to resolve to source code lines; there are several ways of writing them (see [Location Specifications](Location-Specifications.html#Location-Specifications)), but the effect is always to resolve to some source lines to display.

> 一般来说，`list` 命令需要您提供 0、1 或 2 个位置规范。这些位置规范会被解释以解析源代码行；有几种方式可以写它们（参见[位置规范](Location-Specifications.html#Location-Specifications))，但是效果总是解析出一些源代码行来显示。

Here is a complete description of the possible arguments for `list`:

`list locspec`


:   Print lines centered around the line or lines of all the code locations that result from resolving `locspec`.

> 打印从解析`locspec`结果的所有代码位置围绕的行或行。

`list first,last`


:   Print lines from `first` resolve to more than one source line in the program, then the list command shows the list of resolved source lines and does not proceed with the source code listing.

> 如果从`first`解析出的一行代码被解析成多行源代码，那么list命令会显示解析出的源代码行列表，而不会继续列出源代码。

`list ,last`

:   Print lines ending with `last`.

```
Likewise, if `last` resolves to more than one source line in the program, then the list command prints the list of resolved source lines and does not proceed with the source code listing.
```

`list first,`

:   Print lines starting with `first`.

`list +`

:   Print lines just after the lines last printed.

`list -`

:   Print lines just before the lines last printed.

`list`

:   As described in the preceding table.

---

::: header
Next: [Location Specifications](Location-Specifications.html#Location-Specifications)]
:::
