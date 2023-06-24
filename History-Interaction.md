---
tip: translate by openai@2023-06-23 23:07:29
...
---
description: History Interaction (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: History Interaction (Debugging with GDB)
lang: en
resource-type: document
title: History Interaction (Debugging with GDB)
---
::: header

Up: [Using History Interactively](Using-History-Interactively.html#Using-History-Interactively)]

> 上：[交互式使用历史](Using-History-Interactively.html#Using-History-Interactively)]
:::

---

### 34.1 History Expansion


The History library provides a history expansion feature that is similar to the history expansion provided by `csh`. This section describes the syntax used to manipulate the history information.

> 历史库提供了一个类似于csh提供的历史展开功能。本节描述了操纵历史信息所使用的语法。


History expansions introduce words from the history list into the input stream, making it easy to repeat commands, insert the arguments to a previous command into the current input line, or fix errors in previous commands quickly.

> 历史展开引入历史列表中的单词到输入流中，使得重复命令、将上一个命令的参数插入当前输入行或快速修复之前的命令变得容易。


History expansion takes place in two parts. The first is to determine which line from the history list should be used during substitution. The second is to select portions of that line for inclusion into the current one. The line selected from the history is called the *event*, and the portions of that line that are acted upon are called *words*. Various *modifiers* are available to manipulate the selected words. The line is broken into words in the same fashion that Bash does, so that several words surrounded by quotes are considered one word. History expansions are introduced by the appearance of the history expansion character, which is '`!`' by default.

> 历史展开分为两部分。第一部分是确定在替换中使用历史列表中的哪一行。第二部分是选择该行的部分用于当前行中。从历史中选择的行称为*事件*，并且对该行进行操作的部分称为*单词*。有各种*修饰符*可以操作所选择的单词。行以与Bash相同的方式分割为单词，因此几个用引号括起来的单词被视为一个单词。历史展开以历史展开字符的出现引入，默认情况下为'`!`'。


History expansion implements shell-like quoting conventions: a backslash can be used to remove the special handling for the next character; single quotes enclose verbatim sequences of characters, and can be used to inhibit history expansion; and characters enclosed within double quotes may be subject to history expansion, since backslash can escape the history expansion character, but single quotes may not, since they are not treated specially within double quotes.

> 历史扩展实现了类似于shell的引用约定：反斜杠可以用来取消下一个字符的特殊处理；单引号封装文字序列，可以用来禁止历史扩展；双引号中的字符可能会受到历史扩展的影响，因为反斜杠可以转义历史扩展字符，但单引号不行，因为它们在双引号中没有特殊处理。

---


• [Event Designators](Event-Designators.html#Event-Designators):        How to specify which history line to use.

> • [事件指示器](Event-Designators.html#Event-Designators)：如何指定使用哪一行历史记录。

• [Word Designators](Word-Designators.html#Word-Designators):           Specifying which words are of interest.

> • [词语指示器](Word-Designators.html#Word-Designators):           指定哪些单词有兴趣。

• [Modifiers](Modifiers.html#Modifiers):                                Modifying the results of substitution.

> • [修饰符](Modifiers.html#Modifiers)：修改替换结果。

---

---

::: header

Up: [Using History Interactively](Using-History-Interactively.html#Using-History-Interactively)]

> 上：[交互式使用历史](Using-History-Interactively.html#Using-History-Interactively)]
:::
