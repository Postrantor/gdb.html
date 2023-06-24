---
tip: translate by openai@2023-06-23 19:12:28
...
---
description: Commands For Killing (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Commands For Killing (Debugging with GDB)
lang: en
resource-type: document
title: Commands For Killing (Debugging with GDB)
---
::: header
Next: [Numeric Arguments](Numeric-Arguments.html#Numeric-Arguments)]
:::

---

#### 33.4.4 Killing And Yanking

`kill-line (C-k)`


:   Kill the text from point to the end of the line. With a negative numeric argument, kill backward from the cursor to the beginning of the current line.

> 从光标处到行尾杀死文本。使用负数字参数，从光标向后杀死到当前行的开头。

`backward-kill-line (C-x Rubout)`


:   Kill backward from the cursor to the beginning of the current line. With a negative numeric argument, kill forward from the cursor to the end of the current line.

> 从光标开始向后到当前行的开头杀死。使用负数字参数，从光标到当前行的末尾杀死。

`unix-line-discard (C-u)`

:   Kill backward from the cursor to the beginning of the current line.

`kill-whole-line ()`


:   Kill all characters on the current line, no matter where point is. By default, this is unbound.

> 杀死当前行上的所有字符，无论指针在哪里。默认情况下，此功能未绑定。

`kill-word (M-d)`


:   Kill from point to the end of the current word, or if between words, to the end of the next word. Word boundaries are the same as `forward-word`.

> 杀死从当前单词的起点到结尾，或者如果在单词之间，到下一个单词的结尾。单词边界与`forward-word`相同。

`backward-kill-word (M-DEL)`


:   Kill the word behind point. Word boundaries are the same as `backward-word`.

> 杀死点后面的单词。单词边界与`backward-word`相同。

`shell-transpose-words (M-C-t)`


:   Drag the word before point past the word after point, moving point past that word as well. If the insertion point is at the end of the line, this transposes the last two words on the line. Word boundaries are the same as `shell-forward-word` and `shell-backward-word`.

> 将点前的单词拖动到点后的单词之后，并将点移动到该单词之后。如果插入点位于行末，则会交换行末的两个单词。单词边界与`shell-forward-word`和`shell-backward-word`相同。

`unix-word-rubout (C-w)`


:   Kill the word behind point, using white space as a word boundary. The killed text is saved on the kill-ring.

> 杀死点后面的文字，使用空格作为单词边界。被杀死的文字保存在kill-ring中。

`unix-filename-rubout ()`


:   Kill the word behind point, using white space and the slash character as the word boundaries. The killed text is saved on the kill-ring.

> 杀死句号后面的单词，使用空格和斜杠作为单词边界。被杀死的文本保存在kill-ring中。

`delete-horizontal-space ()`

:   Delete all spaces and tabs around point. By default, this is unbound.

`kill-region ()`


:   Kill the text in the current region. By default, this command is unbound.

> 杀死当前区域中的文本。默认情况下，此命令未绑定。

`copy-region-as-kill ()`


:   Copy the text in the region to the kill buffer, so it can be yanked right away. By default, this command is unbound.

> 复制区域中的文本到 kill 缓冲区，这样就可以立即粘贴。默认情况下，此命令未绑定。

`copy-backward-word ()`


:   Copy the word before point to the kill buffer. The word boundaries are the same as `backward-word`. By default, this command is unbound.

> 复制点之前的单词到 kill 缓冲区。单词边界与`backward-word`相同。默认情况下，此命令未绑定。

`copy-forward-word ()`


:   Copy the word following point to the kill buffer. The word boundaries are the same as `forward-word`. By default, this command is unbound.

> 复制点后面的单词到 kill 缓冲区。单词的边界与 `forward-word` 相同。默认情况下，此命令未绑定。

`yank (C-y)`

:   Yank the top of the kill ring into the buffer at point.

`yank-pop (M-y)`


:   Rotate the kill-ring, and yank the new top. You can only do this if the prior command is `yank` or `yank-pop`.

> 旋转kill-ring，并且引用新的顶部。只有在前一个命令是“yank”或“yank-pop”时，你才能这样做。

---

::: header
Next: [Numeric Arguments](Numeric-Arguments.html#Numeric-Arguments)]
:::
