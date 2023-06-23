---
tip: translate by openai@2023-06-23 13:13:05
...
---
description: Setting (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Setting (Debugging with GDB)
lang: en
resource-type: document
title: Setting (Debugging with GDB)
---
::: header
Next: [Show](Show.html#Show)]
:::

---

### 15.1 Switching Between Source Languages


There are two ways to control the working language---either have [GDB] defaults to setting the language automatically. The working language is used to determine how expressions you type are interpreted, how values are printed, etc.

> 有两种方法可以控制工作语言---要么由[GDB]自动设置语言。工作语言用于确定您输入的表达式如何被解释，如何打印值等。


In addition to the working language, every source file that [GDB], but you can set the language associated with a filename extension. See [Displaying the Language](Show.html#Show).

> 除了工作语言外，GDB每个源文件都可以设置与文件扩展名相关联的语言。请参见[显示语言](Show.html#Show)。


This is most commonly a problem when you use a program, such as `cfront` or `f2c`, that generates C but is written in another language. In that case, make the program use `#line` directives in its C output; that way [GDB] will know the correct language of the source code of the original program, and will display that source code, not the generated C code.

> 这通常是使用像`cfront`或`f2c`这样的程序时出现的问题，它们使用其他语言生成C代码。在这种情况下，让程序在其C输出中使用`#line`指令；这样[GDB]就可以知道原始程序的源代码的正确语言，并显示该源代码，而不是生成的C代码。

---


• [Filenames](Filenames.html#Filenames):                    Filename extensions and languages.

> • [文件名](Filenames.html#Filenames):                    文件扩展名和语言。

• [Manually](Manually.html#Manually):                       Setting the working language manually

> • [手动](Manually.html#Manually)：设置工作语言

• [Automatically](Automatically.html#Automatically) infer the source language

> • 自动推断源语言

---

---

::: header
Next: [Show](Show.html#Show)]
:::
