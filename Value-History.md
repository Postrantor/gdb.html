---
tip: translate by openai@2023-06-23 15:22:24
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

> 打印命令打印的值保存在[GDB] *值历史*中。这样您就可以在其他表达式中引用它们。值会一直保留，直到重新读取或丢弃符号表（例如使用`file`或`symbol-file`命令）。当符号表改变时，值历史被丢弃，因为这些值可能包含指向符号表中定义的类型的指针。


The values printed are given *history numbers* by which you can refer to them. These are successive integers starting with one. `print` shows you the history number assigned to a value by printing '`$num = ` is the history number.

> 打印的值是历史数字，您可以参考它们。这些是从1开始的连续整数。`print`会通过打印“$num =”来显示给定值的历史数字。


To refer to any previous value, use '`$` th value from the end; `$$2` is the value just prior to `$$`, `$$1` is equivalent to `$$`, and `$$0` is equivalent to `$`.

> 要引用任何以前的值，使用'`$`值从末尾；`$$2`是刚刚在`$$`之前的值，`$$1`等同于`$$`，而`$$0`等同于`$`。


For example, suppose you have just printed a pointer to a structure and want to see the contents of the structure. It suffices to type

> 例如，假设您刚刚打印了一个指向结构的指针，并希望查看结构的内容。只需要输入

::: smallexample

```bash
p *$
```

:::


If you have a chain of structures where the component `next` points to the next one, you can print the contents of the next one with this:

> 如果你有一个结构链，其中的组件`next`指向下一个，你可以使用这个打印下一个的内容：

::: smallexample

```bash
p *$.next
```

:::


You can print successive links in the chain by repeating this command---which you can do by just typing RET.

> 你可以通过重复这个命令来打印连锁中的连续链接---只需要敲击RET就可以实现。

Note that the history records values, not expressions. If the value of `x` is 4 and you type these commands:

::: smallexample

```bash
print x
set x=5
```

:::


then the value recorded in the value history by the `print` command remains 4 even though the value of `x` has changed.

> 然后，`print`命令记录在值历史中的值仍然为4，即使`x`的值已经改变了。

`show values`


Print the last ten values in the value history, with their item numbers. This is like '`p $$9`' repeated ten times, except that `show values` does not change the history.

> 打印出值历史中的最后十个值及其项目编号。这就像重复十次“p $$9”，但是“show values”不会改变历史记录。

`show values n`


Print ten history values centered on history item number `n`.

> 打印以历史项目编号 n 为中心的十个历史值。

`show values +`


Print ten history values just after the values last printed. If no more values are available, `show values +` produces no display.

> 打印最后一次打印的值之后的十个历史值。如果没有更多的值可用，`show values +`不会有任何显示。


Pressing RET to repeat `show values n` has exactly the same effect as '`show values +`'.

> 按下RET重复“显示值n”与“显示值+”的效果完全相同。

---

::: header
Next: [Convenience Vars](Convenience-Vars.html#Convenience-Vars)]
:::
