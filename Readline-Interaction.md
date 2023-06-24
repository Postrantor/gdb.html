---
tip: translate by openai@2023-06-24 01:55:23
...
---
description: Readline Interaction (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Readline Interaction (Debugging with GDB)
lang: en
resource-type: document
title: Readline Interaction (Debugging with GDB)
---
::: header
Next: [Readline Init File](Readline-Init-File.html#Readline-Init-File)]
:::

---

### 33.2 Readline Interaction


Often during an interactive session you type in a long line of text, only to notice that the first word on the line is misspelled. The Readline library gives you a set of commands for manipulating the text as you type it in, allowing you to just fix your typo, and not forcing you to retype the majority of the line. Using these editing commands, you move the cursor to the place that needs correction, and delete or insert the text of the corrections. Then, when you are satisfied with the line, you simply press RET. You do not have to be at the end of the line to press RET; the entire line is accepted regardless of the location of the cursor within the line.

> 经常在交互式会话中，您输入一长行文本，却发现第一个单词拼写错误。Readline库提供了一组命令，用于在输入文本时操纵文本，允许您只修复拼写错误，而不强迫您重新输入大部分行。使用这些编辑命令，您可以将光标移动到需要纠正的位置，并删除或插入纠正文本。然后，当您对行满意时，只需按RET。您不必在行末尾按RET；无论光标在行中的位置如何，都会接受整行文本。

---


• [Readline Bare Essentials](Readline-Bare-Essentials.html#Readline-Bare-Essentials):              The least you need to know about Readline.

> • [Readline 基本必备](Readline-Bare-Essentials.html#Readline-Bare-Essentials):              你至少需要了解有关Readline的知识。

• [Readline Movement Commands](Readline-Movement-Commands.html#Readline-Movement-Commands):        Moving about the input line.

> • [Readline 移动命令](Readline-Movement-Commands.html#Readline-Movement-Commands):        在输入行中移动。

• [Readline Killing Commands](Readline-Killing-Commands.html#Readline-Killing-Commands):           How to delete text, and how to get it back!

> • [Readline杀死命令](Readline-Killing-Commands.html#Readline-Killing-Commands):           如何删除文本，以及如何恢复它！

• [Readline Arguments](Readline-Arguments.html#Readline-Arguments):                                Giving numeric arguments to commands.

> • [读行参数](Readline-Arguments.html#Readline-Arguments): 给命令提供数字参数。

• [Searching](Searching.html#Searching):                                                           Searching through previous lines.

> • [搜索](Searching.html#Searching): 通过之前的行进行搜索。

---
