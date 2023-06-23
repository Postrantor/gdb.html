---
tip: translate by openai@2023-06-23 12:09:47
...
---
description: Bindable Readline Commands (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Bindable Readline Commands (Debugging with GDB)
lang: en
resource-type: document
title: Bindable Readline Commands (Debugging with GDB)
---
::: header
Next: [Readline vi Mode](Readline-vi-Mode.html#Readline-vi-Mode)]
:::

---

### 33.4 Bindable Readline Commands

---


• [Commands For Moving](Commands-For-Moving.html#Commands-For-Moving):                    Moving about the line.

> • [移动指令](Commands-For-Moving.html#Commands-For-Moving):            在线上移动。

• [Commands For History](Commands-For-History.html#Commands-For-History):                 Getting at previous lines.

> • [历史命令](Commands-For-History.html#Commands-For-History):            获取先前的行。

• [Commands For Text](Commands-For-Text.html#Commands-For-Text):                          Commands for changing text.

> • [文本命令](Commands-For-Text.html#Commands-For-Text)：更改文本的命令。

• [Commands For Killing](Commands-For-Killing.html#Commands-For-Killing):                 Commands for killing and yanking.

> • [杀死的命令](Commands-For-Killing.html#Commands-For-Killing)：命令杀死和拉断。

• [Numeric Arguments](Numeric-Arguments.html#Numeric-Arguments):                          Specifying numeric arguments, repeat counts.

> • [数字参数](Numeric-Arguments.html#Numeric-Arguments): 指定数字参数，重复计数。

• [Commands For Completion](Commands-For-Completion.html#Commands-For-Completion):        Getting Readline to do the typing for you.

> • [完成命令](Commands-For-Completion.html#Commands-For-Completion):        让Readline为您输入。

• [Keyboard Macros](Keyboard-Macros.html#Keyboard-Macros):                                Saving and re-executing typed characters

> • [键盘宏](Keyboard-Macros.html#Keyboard-Macros):  保存和重新执行键入的字符

• [Miscellaneous Commands](Miscellaneous-Commands.html#Miscellaneous-Commands):           Other miscellaneous commands.

> • [杂项命令](Miscellaneous-Commands.html#Miscellaneous-Commands):      其他杂项命令。

---


This section describes Readline commands that may be bound to key sequences. Command names without an accompanying key sequence are unbound by default.

> 这一节描述了可以绑定到按键序列的Readline命令。没有伴随按键序列的命令名默认情况下未绑定。


In the following descriptions, *point* refers to the current cursor position, and *mark* refers to a cursor position saved by the `set-mark` command. The text between the point and mark is referred to as the *region*.

> 在以下描述中，*点*指的是当前光标位置，*标记*指的是通过`set-mark`命令保存的光标位置。点和标记之间的文本被称为*区域*。
