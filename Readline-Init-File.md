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

When a program which uses the Readline library starts up, the init file is read, and the key bindings are set.

In addition, the `C-x C-r` command re-reads this init file, thus incorporating any changes that you might have made to it.

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
