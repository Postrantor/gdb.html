---
tip: translate by openai@2023-06-24 10:41:36
...
---
description: Readline vi Mode (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Readline vi Mode (Debugging with GDB)
lang: en
resource-type: document
title: Readline vi Mode (Debugging with GDB)
---
::: header
Previous: [Bindable Readline Commands](Bindable-Readline-Commands.html#Bindable-Readline-Commands)]
:::

---

### 33.5 Readline vi Mode


While the Readline library does not have a full set of `vi` editing functions, it does contain enough to allow simple editing of the line. The Readline `vi` mode behaves as specified in the [POSIX] standard.

> 虽然Readline库没有完整的vi编辑功能，但它包含足够的功能来允许简单地编辑行。Readline vi模式按照[POSIX]标准指定的方式进行操作。


In order to switch interactively between `emacs` and `vi` editing modes, use the command [M-C-j] (bound to emacs-editing-mode when in `vi` mode and to vi-editing-mode in `emacs` mode). The Readline default is `emacs` mode.

> 要在emacs和vi编辑模式之间交互切换，请使用[M-C-j]命令（在vi模式下绑定到emacs-editing-mode，在emacs模式下绑定到vi-editing-mode）。Readline的默认模式是emacs模式。


When you enter a line in `vi` mode, you are already placed in 'insertion' mode, as if you had typed an '`i`', and so forth.

> 当你在vi模式下输入一行时，你已经处于插入模式，就好像你输入了一个“i”，等等。
