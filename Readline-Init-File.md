---
tip: translate by openai@2023-06-24 01:55:04
...
---
description: Readline Init File (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Readline Init File (Debugging with GDB)
lang: en
resource-type: document
title: Readline Init File (Debugging with GDB)
---
::: header
Next: [Bindable Readline Commands](Bindable-Readline-Commands.html#Bindable-Readline-Commands)]
:::

---

### 33.3 Readline Init File


Although the Readline library comes with a set of Emacs-like keybindings installed by default, it is possible to use a different set of keybindings. Any user can customize programs that use Readline by putting commands in an *inputrc* file, conventionally in his home directory. The name of this file is taken from the value of the environment variable `INPUTRC`. If that variable is unset, the default is `~/.inputrc`.

> 虽然Readline库默认安装了一组类似Emacs的键绑定，但也可以使用不同的键绑定。任何用户都可以通过在*inputrc*文件中放置命令来自定义使用Readline的程序，通常放置在其主目录中。此文件的名称来自环境变量`INPUTRC`的值。如果该变量未设置，则默认值为`~/.inputrc`。


When a program which uses the Readline library starts up, the init file is read, and the key bindings are set.

> 当使用Readline库的程序启动时，会读取初始文件，并设置按键绑定。


In addition, the `C-x C-r` command re-reads this init file, thus incorporating any changes that you might have made to it.

> 此外，`C-x C-r`命令会重新读取此初始文件，从而将您可能对其所做的任何更改都纳入其中。

+:--------------------------------------------------------------------------------------------------------------+-----------------------+:----------------------------------------------+
| • [Readline Init File Syntax](Readline-Init-File-Syntax.html#Readline-Init-File-Syntax):       |                       | Syntax for the commands in the inputrc file.  |
+---------------------------------------------------------------------------------------------------------------+-----------------------+-----------------------------------------------+
| ``menu-comment                                                                                              |                       |                                               | |``                                                                                                           |                       |                                               |
+---------------------------------------------------------------------------------------------------------------+-----------------------+-----------------------------------------------+
| • [Conditional Init Constructs](Conditional-Init-Constructs.html#Conditional-Init-Constructs): |                       | Conditional key bindings in the inputrc file. |
+---------------------------------------------------------------------------------------------------------------+-----------------------+-----------------------------------------------+
| ``menu-comment                                                                                              |                       |                                               | |``                                                                                                           |                       |                                               |
+---------------------------------------------------------------------------------------------------------------+-----------------------+-----------------------------------------------+
| • [Sample Init File](Sample-Init-File.html#Sample-Init-File):                                  |                       | An example inputrc file.                      |
+---------------------------------------------------------------------------------------------------------------+-----------------------+-----------------------------------------------+
