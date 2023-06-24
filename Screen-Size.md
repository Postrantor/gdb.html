---
tip: translate by openai@2023-06-24 02:18:45
...
---
description: Screen Size (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Screen Size (Debugging with GDB)
lang: en
resource-type: document
title: Screen Size (Debugging with GDB)
---
::: header
Next: [Output Styling](Output-Styling.html#Output-Styling)]
:::

---

### 22.4 Screen Size


Certain commands to [GDB] tries to break the line at a readable place, rather than simply letting it overflow onto the following line.

> GDB 的某些命令试图在可读的地方断行，而不是简单地将其溢出到下一行。


Normally [GDB] uses the termcap data base together with the value of the `TERM` environment variable and the `stty rows` and `stty cols` settings. If this is not correct, you can override it with the `set height` and `set width` commands:

> 一般来说，[GDB]会使用termcap数据库，以及`TERM`环境变量的值、`stty rows`和`stty cols`设置。如果不正确，可以使用`set height`和`set width`命令来覆盖它。

`set height lpp`

`set height unlimited`

`show height`

`set width cpl`

`set width unlimited`

`show width`


These `set` commands specify a screen height of `lpp` characters. The associated `show` commands display the current settings.

> 这些`set`命令指定一个屏幕高度为`lpp`字符。相关的`show`命令显示当前设置。


If you specify a height of either `unlimited` or zero lines, [GDB] does not pause during output no matter how long the output is. This is useful if output is to a file or to an editor buffer.

> 如果您指定的高度为“无限”或零行，[GDB]无论输出有多长，都不会在输出期间暂停。如果输出到文件或编辑器缓冲区，这将非常有用。


Likewise, you can specify '`set width unlimited` from wrapping its output.

> 同样，你可以指定'设置宽度无限'以避免其输出被换行。

`set pagination on`

`set pagination off`


Turn the output pagination on or off; the default is on. Turning pagination off is the alternative to `set height unlimited`. Note that running [GDB] option (see [-batch](Mode-Options.html#Mode-Options)) also automatically disables pagination.

> 打开或关闭输出分页；默认情况下打开。关闭分页是替代`设置高度无限`的另一种方式。请注意，运行[GDB]选项（参见[-batch]（Mode-Options.html#Mode-Options））也会自动禁用分页。

`show pagination`

Show the current pagination mode.

---

::: header
Next: [Output Styling](Output-Styling.html#Output-Styling)]
:::
