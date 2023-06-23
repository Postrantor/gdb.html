---
description: Commands For Moving (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Commands For Moving (Debugging with GDB)
lang: en
resource-type: document
title: Commands For Moving (Debugging with GDB)
---
::: header
Next: [Commands For History](Commands-For-History.html#Commands-For-History)]
:::

---

#### 33.4.1 Commands For Moving

`beginning-of-line (C-a)`

:   Move to the start of the current line.

`end-of-line (C-e)`

:   Move to the end of the line.

`forward-char (C-f)`

:   Move forward a character.

`backward-char (C-b)`

:   Move back a character.

`forward-word (M-f)`

:   Move forward to the end of the next word. Words are composed of letters and digits.

`backward-word (M-b)`

:   Move back to the start of the current or previous word. Words are composed of letters and digits.

`previous-screen-line ()`

:   Attempt to move point to the same physical screen column on the previous physical screen line. This will not have the desired effect if the current Readline line does not take up more than one physical line or if point is not greater than the length of the prompt plus the screen width.

`next-screen-line ()`

:   Attempt to move point to the same physical screen column on the next physical screen line. This will not have the desired effect if the current Readline line does not take up more than one physical line or if the length of the current Readline line is not greater than the length of the prompt plus the screen width.

`clear-display (M-C-l)`

:   Clear the screen and, if possible, the terminal's scrollback buffer, then redraw the current line, leaving the current line at the top of the screen.

`clear-screen (C-l)`

:   Clear the screen, then redraw the current line, leaving the current line at the top of the screen.

`redraw-current-line ()`

:   Refresh the current line. By default, this is unbound.

---

::: header
Next: [Commands For History](Commands-For-History.html#Commands-For-History)]
:::
