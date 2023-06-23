---
tip: translate by openai@2023-06-23 12:35:46
...
---
description: Screen Size (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Screen Size (Debugging with GDB)
lang: en
resource-type: document
title: Screen Size (Debugging with GDB)
---------------------------------------

::: header
Next: [Output Styling](Output-Styling.html#Output-Styling)]
:::

---

### 22.4 Screen Size

Certain commands to [GDB] tries to break the line at a readable place, rather than simply letting it overflow onto the following line.

> 某些 GDB 命令会尝试在一个可读的位置断行，而不是简单地让它溢出到下一行。

Normally [GDB] uses the termcap data base together with the value of the `TERM` environment variable and the `stty rows` and `stty cols` settings. If this is not correct, you can override it with the `set height` and `set width` commands:

> 通常，GDB 会使用 termcap 数据库，以及环境变量 `TERM`、`stty rows` 和 `stty cols` 的值。如果不正确，你可以使用 `set height` 和 `set width` 命令来覆盖它。

`set height lpp`

`set height unlimited`

`show height`

`set width cpl`

`set width unlimited`

`show width`

These `set` commands specify a screen height of `lpp` characters. The associated `show` commands display the current settings.

> 这些 `set` 命令指定一个屏幕高度为 `lpp` 个字符。相关的 `show` 命令显示当前设置。

If you specify a height of either `unlimited` or zero lines, [GDB] does not pause during output no matter how long the output is. This is useful if output is to a file or to an editor buffer.

> 如果您指定的高度为 `unlimited` 或零行，[GDB]不会根据输出的长度而暂停。 如果输出到文件或编辑器缓冲区，这是有用的。

Likewise, you can specify '`set width unlimited` from wrapping its output.

> 同样，您可以通过设置“宽度无限”来避免其输出被换行。

`set pagination on`

`set pagination off`

Turn the output pagination on or off; the default is on. Turning pagination off is the alternative to `set height unlimited`. Note that running [GDB] option (see [-batch](Mode-Options.html#Mode-Options)) also automatically disables pagination.

> 开启或关闭输出分页；默认是开启的。关闭分页是取代 `设置无限高度` 的另一种方式。请注意，运行[GDB]选项（参见[-batch](Mode-Options.html#Mode-Options)）也会自动禁用分页。

`show pagination`

Show the current pagination mode.

> 显示当前的分页模式。

---

::: header
Next: [Output Styling](Output-Styling.html#Output-Styling)]
:::
