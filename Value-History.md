---
tip: translate by openai@2023-06-24 04:33:25
...
---
description: Value History (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Value History (Debugging with GDB)
lang: en
resource-type: document
title: Value History (Debugging with GDB)
---
::: header
Next: [Convenience Vars](Convenience-Vars.html#Convenience-Vars)]
:::

---

### 10.11 Value History


Values printed by the `print` command are saved in the [GDB] *value history*. This allows you to refer to them in other expressions. Values are kept until the symbol table is re-read or discarded (for example with the `file` or `symbol-file` commands). When the symbol table changes, the value history is discarded, since the values may contain pointers back to the types defined in the symbol table.

> 打印命令打印的值保存在GDB值历史中，这样可以在其他表达式中引用它们。除非重新读取或丢弃符号表（例如使用“file”或“symbol-file”命令），否则保留这些值。当符号表改变时，值历史被丢弃，因为这些值可能包含指向符号表中定义的类型的指针。


The values printed are given *history numbers* by which you can refer to them. These are successive integers starting with one. `print` shows you the history number assigned to a value by printing '`$num = ` is the history number.

> 打印出来的值对应着历史编号，这些编号是从1开始的连续整数。`print`会通过打印“$num =”来显示某个值对应的历史编号。


To refer to any previous value, use '`$` th value from the end; `$$2` is the value just prior to `$$`, `$$1` is equivalent to `$$`, and `$$0` is equivalent to `$`.

> 要引用任何以前的值，请使用“$”最后一个值；“$$2”是刚刚在“$$”之前的值，“$$1”等同于“$$”，而“$$0”等同于“$”。


For example, suppose you have just printed a pointer to a structure and want to see the contents of the structure. It suffices to type

> 例如，假设您刚打印了一个指向结构的指针，并希望查看结构的内容。只需键入

::: smallexample

```bash
p *$
```

:::


If you have a chain of structures where the component `next` points to the next one, you can print the contents of the next one with this:

> 如果您有一个结构链，其中组件`next`指向下一个，您可以使用此功能打印下一个的内容：

::: smallexample

```bash
p *$.next
```

:::


You can print successive links in the chain by repeating this command---which you can do by just typing RET.

> 你可以通过重复这个命令来打印链中的连续链接---你可以通过只键入RET来完成。


Note that the history records values, not expressions. If the value of `x` is 4 and you type these commands:

> 注意，历史记录的是值，而不是表达式。如果x的值为4，并且你输入了这些命令：

::: smallexample

```bash
print x
set x=5
```

:::


then the value recorded in the value history by the `print` command remains 4 even though the value of `x` has changed.

> 那么，即使`x`的值已经改变，由`print`命令记录在值历史中的值仍然是4。

`show values`


Print the last ten values in the value history, with their item numbers. This is like '`p $$9`' repeated ten times, except that `show values` does not change the history.

> 打印值历史中的最后十个值及其项目编号。这就像重复十次“p $$9”，只是“显示值”不会改变历史记录。

`show values n`

Print ten history values centered on history item number `n`.

`show values +`


Print ten history values just after the values last printed. If no more values are available, `show values +` produces no display.

> 打印出最后一次打印出的值之后的十个历史值。如果没有更多的值可用，`show values +`不会显示任何内容。


Pressing RET to repeat `show values n` has exactly the same effect as '`show values +`'.

> 按下RET重复“show values n”的效果与“show values +”完全相同。

---

::: header
Next: [Convenience Vars](Convenience-Vars.html#Convenience-Vars)]
:::
