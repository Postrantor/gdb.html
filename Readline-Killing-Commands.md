---
tip: translate by openai@2023-06-24 01:56:00
...
---
description: Readline Killing Commands (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Readline Killing Commands (Debugging with GDB)
lang: en
resource-type: document
title: Readline Killing Commands (Debugging with GDB)
---
::: header
Next: [Readline Arguments](Readline-Arguments.html#Readline-Arguments)]
:::

---

#### 33.2.3 Readline Killing Commands


*Killing* text means to delete the text from the line, but to save it away for later use, usually by *yanking* (re-inserting) it back into the line. ('Cut' and 'paste' are more recent jargon for 'kill' and 'yank'.)

> *杀死*文本的意思是从行中删除文本，但可以保存起来以备日后使用，通常是通过*拉出*（重新插入）它回到行中。 （“剪切”和“粘贴”是最近有关“杀死”和“拉出”的行话。）


If the description for a command says that it 'kills' text, then you can be sure that you can get the text back in a different (or the same) place later.

> 如果一个命令的描述说它“杀死”文本，那么你可以确定你可以稍后在不同（或相同）的位置获取文本。


When you use a kill command, the text is saved in a *kill-ring*. Any number of consecutive kills save all of the killed text together, so that when you yank it back, you get it all. The kill ring is not line specific; the text that you killed on a previously typed line is available to be yanked back later, when you are typing another line.

> 当你使用kill命令时，文本会被保存在*kill-ring*中。任何连续的kill都会把所有被杀死的文本保存在一起，这样当你把它拉回来时，你就可以得到它的全部内容。 kill ring不是特定于行的；你在先前输入的行上杀死的文本在你输入另一行时仍然可以被拉回来。

Here is the list of commands for killing text.

[C-k]


:   Kill the text from the current cursor position to the end of the line.

> 从当前光标位置到行末尾删除文本。

[M-d]


:   Kill from the cursor to the end of the current word, or, if between words, to the end of the next word. Word boundaries are the same as those used by [M-f].

> 从光标到当前单词的末尾（或者，如果在单词之间，到下一个单词的末尾）删除。单词边界与[M-f]使用的相同。

[M-[DEL]


:   Kill from the cursor the start of the current word, or, if between words, to the start of the previous word. Word boundaries are the same as those used by [M-b].

> 从光标开始删除当前单词的开头，或者如果在单词之间，则删除上一个单词的开头。单词边界与[M-b]使用的相同。

[C-w]


:   Kill from the cursor to the previous whitespace. This is different than [M-[DEL] because the word boundaries differ.

> 从光标开始到上一个空格结束删除。这与[M-[DEL]不同，因为单词的边界不同。


Here is how to *yank* the text back into the line. Yanking means to copy the most-recently-killed text from the kill buffer.

> 这是如何将文本*拉回*行中的方法。拉回意味着从 kill 缓冲区复制最近被删除的文本。

[C-y]


:   Yank the most recently killed text back into the buffer at the cursor.

> 把最近删除的文本插入光标处的缓冲区中。

[M-y]


:   Rotate the kill-ring, and yank the new top. You can only do this if the prior command is [C-y].

> 旋转 kill-ring，并引用新的顶部。只有在之前的命令是[C-y]时，你才能这样做。

---

::: header
Next: [Readline Arguments](Readline-Arguments.html#Readline-Arguments)]
:::
