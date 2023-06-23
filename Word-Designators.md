---
tip: translate by openai@2023-06-23 15:41:29
...
---
description: Word Designators (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Word Designators (Debugging with GDB)
lang: en
resource-type: document
title: Word Designators (Debugging with GDB)
---
::: header
Next: [Modifiers](Modifiers.html#Modifiers)]
:::

---

#### 34.1.2 Word Designators


Word designators are used to select desired words from the event. A '`:`'. Words are numbered from the beginning of the line, with the first word being denoted by 0 (zero). Words are inserted into the current line separated by single spaces.

> 字詞標記用於從事件中選擇所需的字詞。 '`：`'。從行開頭開始編號字詞，第一個字詞用0（零）表示。字詞以單個空格插入當前行。

For example,

`!!`


:   designates the preceding command. When you type this, the preceding command is repeated in toto.

> ": 表示前一个命令。当你输入这个时，前一个命令将完全重复。

`!!:$`


:   designates the last argument of the preceding command. This may be shortened to `!$`.

> `:`表示前一个命令的最后一个参数。这可以简写为`!$`。

`!fi:2`


:   designates the second argument of the most recent command starting with the letters `fi`.

> ": 指定最近以"fi"开头的命令的第二个参数。


Here are the word designators:

> 这些是词语指示符：

`0 (zero)`


:   The `0` th word. For many applications, this is the command word.

> 这个`0`号单词。对许多应用程序来说，这是指令词。

`n`

:   The `n` th word.

`^`


:   The first argument; that is, word 1.

> 第一个参数；也就是第一个词。

`$`

:   The last argument.

`%`


:   The first word matched by the most recent '`?string?`' search, if the search string begins with a character that is part of a word.

> 最近的“？字符串？”搜索匹配到的第一个单词，如果搜索字符串以一个单词的一部分开头。

`x-y`


:   A range of words; '`-y`'.

> 一系列的字；“-y”。

`*`


:   All of the words, except the `0` th. This is a synonym for '`1-$`' if there is just one word in the event; the empty string is returned in that case.

> 所有的单词，除了第0个。如果只有一个单词在事件中，这是“1-$”的同义词；在这种情况下，返回空字符串。

`x*`

:   Abbreviates '`x-$`'

`x-`


:   Abbreviates '`x-$`' is missing, it defaults to 0.

> 缩写'x-$'缺失，默认为0。


If a word designator is supplied without an event specification, the previous command is used as the event.

> 如果提供了字词标识符而没有指定事件，则将上一个命令用作事件。

---

::: header
Next: [Modifiers](Modifiers.html#Modifiers)]
:::
