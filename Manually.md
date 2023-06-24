---
tip: translate by openai@2023-06-24 00:12:39
...
---
description: Manually (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Manually (Debugging with GDB)
lang: en
resource-type: document
title: Manually (Debugging with GDB)
---
::: header
Next: [Automatically](Automatically.html#Automatically)]
:::

---

#### 15.1.2 Setting the Working Language


If you allow [GDB] to set the language automatically, expressions are interpreted the same way in your debugging session and your program.

> 如果您允许GDB自动设置语言，则表达式在您的调试会话和程序中的解释是相同的。


If you wish, you may set the language manually. To do this, issue the command '`set language lang`'.

> 如果您愿意，可以手动设置语言。要做到这一点，请输入命令“设置语言lang”。


Setting the language manually prevents [GDB] was parsing Modula-2, a command such as:

> 手动设置语言可以防止[GDB]解析Modula-2，例如：

::: smallexample

```bash
print a = b + c
```

:::


might not have the effect you intended. In C, this means to add `b` and `c` and place the result in `a`. The result printed would be the value of `a`. In Modula-2, this means to compare `a` to the result of `b+c`, yielding a `BOOLEAN` value.

> 可能没有你所期望的效果。在C语言中，这意味着要将`b`和`c`相加，并将结果放入`a`中。打印的结果将是`a`的值。在Modula-2中，这意味着要将`a`与`b+c`的结果进行比较，得出一个`BOOLEAN`值。
