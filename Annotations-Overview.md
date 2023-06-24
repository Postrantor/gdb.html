---
tip: translate by openai@2023-06-23 17:17:18
...
---
description: Annotations Overview (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Annotations Overview (Debugging with GDB)
lang: en
resource-type: document
title: Annotations Overview (Debugging with GDB)
---
::: header
Next: [Server Prefix](Server-Prefix.html#Server-Prefix)]
:::

---

### 28.1 What is an Annotation?


Annotations start with a newline character, two '`control-z`' characters, and the name of the annotation. If there is no additional information associated with this annotation, the name of the annotation is followed immediately by a newline. If there is additional information, the name of the annotation is followed by a space, the additional information, and a newline. The additional information cannot contain newline characters.

> 注释以一个新行字符、两个'control-z'字符和注释名称开头。如果没有与此注释相关的其他信息，则注释名称后面立即跟一个新行。如果有其他信息，注释名称后面跟一个空格、其他信息和一个新行。其他信息不能包含换行符。


Any output not beginning with a newline and two '`control-z`' annotation which means those three characters as output.

> 任何输出不以换行符和两个“控制Z”注释开头，这意味着这三个字符作为输出。


The annotation `level`, and level 2 annotations have been made obsolete (see [Limitations of the Annotation Interface](../annotate/Limitations.html#Limitations) in GDB's Obsolete Annotations).

> 标注`level`和第2级标注已被弃用（参见GDB的弃用标注中的[标注界面的局限性](../annotate/Limitations.html#Limitations)）。

`set annotate level`

The [GDB].

`show annotate`


Show the current annotation level.

> 显示当前注释级别。


This chapter describes level 3 annotations.

> 本章节描述第三级注释。


A simple example of starting up [GDB] with annotations is:

> 一个启动GDB并注释的简单示例是：

::: smallexample

```bash
$ gdb --annotate=3
GNU gdb 6.0
Copyright 2003 Free Software Foundation, Inc.
GDB is free software, covered by the GNU General Public License,
and you are welcome to change it and/or distribute copies of it
under certain conditions.
Type "show copying" to see the conditions.
There is absolutely no warranty for GDB.  Type "show warranty"
for details.
This GDB was configured as "i386-pc-linux-gnu"

^Z^Zpre-prompt
(gdb)
^Z^Zprompt
quit

^Z^Zpost-prompt
$
```

:::

Here '`quit`.

---

::: header
Next: [Server Prefix](Server-Prefix.html#Server-Prefix)]
:::
