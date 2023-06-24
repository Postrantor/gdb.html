---
tip: translate by openai@2023-06-23 19:13:47
...
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

> 向前移动到下一个单词的末尾。单词由字母和数字组成。

`backward-word (M-b)`


:   Move back to the start of the current or previous word. Words are composed of letters and digits.

> 回到当前或上一个单词的开头。单词由字母和数字组成。

`previous-screen-line ()`


:   Attempt to move point to the same physical screen column on the previous physical screen line. This will not have the desired effect if the current Readline line does not take up more than one physical line or if point is not greater than the length of the prompt plus the screen width.

> 尝试将光标移动到上一个物理屏幕行的相同物理屏幕列上。如果当前的Readline行不超过一个物理行或者光标位置不大于提示符长度加上屏幕宽度，则不会产生期望的效果。

`next-screen-line ()`


:   Attempt to move point to the same physical screen column on the next physical screen line. This will not have the desired effect if the current Readline line does not take up more than one physical line or if the length of the current Readline line is not greater than the length of the prompt plus the screen width.

> 尝试将指针移动到下一个物理屏幕行的相同物理屏幕列。如果当前的Readline行不超过一个物理行或者当前的Readline行的长度不大于提示符加屏幕宽度，则不会产生预期的效果。

`clear-display (M-C-l)`


:   Clear the screen and, if possible, the terminal's scrollback buffer, then redraw the current line, leaving the current line at the top of the screen.

> 清除屏幕，如果可能的话，也清除终端的滚动缓冲区，然后重新绘制当前行，使当前行位于屏幕顶部。

`clear-screen (C-l)`


:   Clear the screen, then redraw the current line, leaving the current line at the top of the screen.

> 清除屏幕，然后重绘当前行，将当前行保留在屏幕顶部。

`redraw-current-line ()`

:   Refresh the current line. By default, this is unbound.

---

::: header
Next: [Commands For History](Commands-For-History.html#Commands-For-History)]
:::
