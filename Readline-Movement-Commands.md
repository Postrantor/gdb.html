---
description: Readline Movement Commands (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Readline Movement Commands (Debugging with GDB)
lang: en
resource-type: document
title: Readline Movement Commands (Debugging with GDB)
---
::: header
Next: [Readline Killing Commands](Readline-Killing-Commands.html#Readline-Killing-Commands)]
:::

---

#### 33.2.2 Readline Movement Commands

The above table describes the most basic keystrokes that you need in order to do editing of the input line. For your convenience, many other commands have been added in addition to [C-b], and DEL. Here are some commands for moving more rapidly about the line.

[C-a]

:   Move to the start of the line.

[C-e]

:   Move to the end of the line.

[M-f]

:   Move forward a word, where a word is composed of letters and digits.

[M-b]

:   Move backward a word.

[C-l]

:   Clear the screen, reprinting the current line at the top.

Notice how [C-f] moves forward a word. It is a loose convention that control keystrokes operate on characters while meta keystrokes operate on words.
