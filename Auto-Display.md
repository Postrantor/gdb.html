---
tip: translate by openai@2023-06-23 17:39:46
...
---
description: Auto Display (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Auto Display (Debugging with GDB)
lang: en
resource-type: document
title: Auto Display (Debugging with GDB)
---
::: header
Next: [Print Settings](Print-Settings.html#Print-Settings)]
:::

---

### 10.8 Automatic Display


If you find that you want to print the value of an expression frequently (to see how it changes), you might want to add it to the *automatic display list* so that [GDB] prints its value each time your program stops. Each expression added to the list is given a number to identify it; to remove an expression from the list, you specify that number. The automatic display looks like this:

> 如果你发现你经常需要打印表达式的值（看它是如何改变的），你可能希望把它添加到*自动显示列表*中，这样[GDB]就会在你的程序停止时打印它的值。每个添加到列表中的表达式都会被给予一个编号来标识它；要从列表中移除一个表达式，你只需指定该编号。自动显示看起来像这样：

::: smallexample

```bash
2: foo = 38
3: bar[5] = (struct hack *) 0x3804
```

:::


This display shows item numbers, expressions and their current values. As with displays you request manually using `x` or `print`, you can specify the output format you prefer; in fact, `display` decides whether to use `print` or `x` depending your format specification---it uses `x` if you specify either the '`i`' format, or a unit size; otherwise it uses `print`.

> 这个显示器显示了项目编号、表达式和它们当前的值。与使用`x`或`print`手动请求的显示器一样，您可以指定您喜欢的输出格式；实际上，`display`根据您的格式规范来决定是使用`print`还是`x`---如果指定了“i”格式或单位大小，则使用`x`，否则使用`print`。

`display expr`


Add the expression `expr` to the list of expressions to display each time your program stops. See [Expressions](Expressions.html#Expressions).

> 将表达式`expr`添加到每次程序停止时显示的表达式列表中。请参阅[表达式](Expressions.html#Expressions)。

`display` does not repeat if you press RET again after using it.

`display/fmt expr`


For `fmt`. See [Output Formats](Output-Formats.html#Output-Formats).

> 对于`fmt`，请参阅[输出格式](Output-Formats.html#Output-Formats)。

`display/fmt addr`


For `fmt`'. See [Examining Memory](Memory.html#Memory).

> 查看[检查内存](Memory.html#Memory)，关于`fmt`。


For example, '`display/i $pc`' is a common name for the program counter; see [Registers](Registers.html#Registers)).

> 例如，“display/i $pc”是程序计数器的常用名称；参见[寄存器](Registers.html#Registers)。

`undisplay dnums…`

`delete display dnums…`


Remove items from the list of expressions to display. Specify the numbers of the displays that you want affected with the command argument `dnums`' display; or it could be a range of display numbers, as in `2-4`.

> 從表達式列表中移除項目。使用命令參數`dnums`指定您想要影響的顯示編號; 或者可以是一個顯示編號範圍，如`2-4`。

`undisplay` does not repeat if you press RET after using it. (Otherwise you would just get the error '`No display number …`'.)

`disable display dnums…`


Disable the display of item numbers `dnums`' display; or it could be a range of display numbers, as in `2-4`.

> 禁用项目编号`dnums`的显示; 或者可以是一系列的显示编号，如`2-4`。

`enable display dnums…`


Enable display of item numbers `dnums`' display; or it could be a range of display numbers, as in `2-4`.

> 启用项目编号`dnums`的显示；或者可以是显示编号的范围，如`2-4`。

`display`


Display the current values of the expressions on the list, just as is done when your program stops.

> 显示列表中表达式的当前值，就像程序停止时一样。

`info display`


Print the list of expressions previously set up to display automatically, each one with its item number, but without showing the values. This includes disabled expressions, which are marked as such. It also includes expressions which would not be displayed right now because they refer to automatic variables not currently available.

> 打印出之前设置好的表达式列表，每一个都有对应的项目编号，但不显示其值。这包括被禁用的表达式，它们会被标记出来。它也包括当前不会显示的表达式，因为它们引用的是当前不可用的自动变量。


If a display expression refers to local variables, then it does not make sense outside the lexical context for which it was set up. Such an expression is disabled when execution enters a context where one of its variables is not defined. For example, if you give the command `display last_char` while inside a function with an argument `last_char`, [GDB] displays this argument while your program continues to stop inside that function. When it stops elsewhere---where there is no variable `last_char`---the display is disabled automatically. The next time your program stops where `last_char` is meaningful, you can enable the display expression once again.

> 如果显示表达式引用本地变量，那么它在其设置的词法上下文之外就没有意义了。当执行进入一个其中一个变量未定义的上下文时，这样的表达式就会被禁用。例如，如果你在一个有参数`last_char`的函数内输入`display last_char`的命令，[GDB]会在你的程序在该函数内停止时显示这个参数。当它在没有变量`last_char`的其它位置停止时，显示表达式会自动被禁用。下一次你的程序在`last_char`有意义的位置停止时，你可以再次启用显示表达式。

---

::: header
Next: [Print Settings](Print-Settings.html#Print-Settings)]
:::
