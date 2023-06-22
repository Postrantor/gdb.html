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

In order to switch interactively between `emacs` and `vi` editing modes, use the command [M-C-j] (bound to emacs-editing-mode when in `vi` mode and to vi-editing-mode in `emacs` mode). The Readline default is `emacs` mode.

When you enter a line in `vi` mode, you are already placed in 'insertion' mode, as if you had typed an '`i`', and so forth.
