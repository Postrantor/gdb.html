---
tip: translate by openai@2023-06-23 14:27:49
...
---
description: The Print Command with Objective-C (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: The Print Command with Objective-C (Debugging with GDB)
lang: en
resource-type: document
title: The Print Command with Objective-C (Debugging with GDB)
---
::: header
Previous: [Method Names in Commands](Method-Names-in-Commands.html#Method-Names-in-Commands)]
:::

---

#### 15.4.4.2 The Print Command With Objective-C


The print command has also been extended to accept methods. For example:

> 打印命令也已经扩展以接受方法。例如：

::: smallexample

```bash
print -[object hash]
```

:::


will tell [GDB] and print the result. Also, an additional command has been added, `print-object` or `po` for short, which is meant to print the description of an object. However, this command may only work with certain Objective-C libraries that have a particular hook function, `_NSPrintForDebugger`, defined.

> 将[GDB]告知并打印结果。另外，还添加了一个附加命令`print-object`或简称`po`，用于打印对象的描述。但是，此命令可能仅适用于具有特定钩子函数`_NSPrintForDebugger`定义的某些Objective-C库。
