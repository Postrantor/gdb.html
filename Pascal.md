---
tip: translate by openai@2023-06-24 01:05:05
...
---
description: Pascal (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Pascal (Debugging with GDB)
lang: en
resource-type: document
title: Pascal (Debugging with GDB)
---
::: header
Next: [Rust](Rust.html#Rust)]
:::

---

#### 15.4.7 Pascal


Debugging Pascal programs which use sets, subranges, file variables, or nested functions does not currently work. [GDB] does not support entering expressions, printing values, or similar features using Pascal syntax.

> 调试使用集合、子范围、文件变量或嵌套函数的Pascal程序目前不起作用。[GDB]不支持使用Pascal语法输入表达式、打印值或类似功能。


The Pascal-specific command `set print pascal_static-members` controls whether static members of Pascal objects are displayed. See [pascal_static-members](Print-Settings.html#Print-Settings).

> 命令`set print pascal_static-members`控制是否显示Pascal对象的静态成员。参见[pascal_static-members](Print-Settings.html#Print-Settings)。
