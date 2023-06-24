---
tip: translate by openai@2023-06-24 01:52:23
...
---
description: Readline Bare Essentials (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Readline Bare Essentials (Debugging with GDB)
lang: en
resource-type: document
title: Readline Bare Essentials (Debugging with GDB)
---
::: header
Next: [Readline Movement Commands](Readline-Movement-Commands.html#Readline-Movement-Commands)]
:::

---

#### 33.2.1 Readline Bare Essentials


In order to enter characters into the line, simply type them. The typed character appears where the cursor was, and then the cursor moves one space to the right. If you mistype a character, you can use your erase character to back up and delete the mistyped character.

> 要输入字符到行中，只需要打出它们即可。打出的字符会出现在光标所在的位置，然后光标会向右移动一个空格。如果你打错了字符，你可以使用擦除字符来回退并删除错误的字符。


Sometimes you may mistype a character, and not notice the error until you have typed several other characters. In that case, you can type [C-b].

> 有时你可能会打错一个字符，而不会注意到错误，直到你已经输入了其他几个字符。在这种情况下，你可以输入[C-b]。


When you add text in the middle of a line, you will notice that characters to the right of the cursor are 'pushed over' to make room for the text that you have inserted. Likewise, when you delete text behind the cursor, characters to the right of the cursor are 'pulled back' to fill in the blank space created by the removal of the text. A list of the bare essentials for editing the text of an input line follows.

> 当您在行中间添加文本时，您会注意到光标右侧的字符被“推开”以留出您插入的文本的空间。 同样，当您删除光标后面的文本时，光标右侧的字符会被“拉回”以填补由文本删除而产生的空白空间。 以下是编辑输入行文本的必备要素的列表。

[C-b]

:   Move back one character.

[C-f]

:   Move forward one character.

DEL or Backspace

:   Delete the character to the left of the cursor.

[C-d]

:   Delete the character underneath the cursor.

Printing characters

:   Insert the character into the line at the cursor.

[C-_]


:   Undo the last editing command. You can undo all the way back to an empty line.

> 撤销上一次编辑命令。您可以撤销一直回到空白行。


(Depending on your configuration, the Backspace key be set to delete the character to the left of the cursor and the DEL key set to delete the character underneath the cursor, like [C-d], rather than the character to the left of the cursor.)

> 根据您的配置，Backspace键可以设置为删除光标左侧的字符，而DEL键可以设置为删除光标下方的字符，就像[C-d]那样，而不是光标左侧的字符。

---

::: header
Next: [Readline Movement Commands](Readline-Movement-Commands.html#Readline-Movement-Commands)]
:::
