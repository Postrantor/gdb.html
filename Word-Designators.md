---
tip: translate by openai@2023-06-24 04:46:32
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

> 字词指示器用于从事件中选择所需的单词。一个'`:`'。从行开头开始给单词编号，第一个单词用0（零）表示。单词以单个空格插入当前行中。

For example,

`!!`


:   designates the preceding command. When you type this, the preceding command is repeated in toto.

> ": 表示前面的命令。当你输入这个时，前面的命令会完整地重复一遍。

`!!:$`


:   designates the last argument of the preceding command. This may be shortened to `!$`.

> `:`表示前一个命令的最后一个参数。这可以缩写为`!$`。

`!fi:2`


:   designates the second argument of the most recent command starting with the letters `fi`.

> ': 指定最近以字母'fi'开头的命令的第二个参数。

Here are the word designators:

`0 (zero)`

:   The `0` th word. For many applications, this is the command word.

`n`

:   The `n` th word.

`^`

:   The first argument; that is, word 1.

`$`

:   The last argument.

`%`


:   The first word matched by the most recent '`?string?`' search, if the search string begins with a character that is part of a word.

> 最近的“？字符串？”搜索匹配到的第一个单词，如果搜索字符串以一个字符开头，该字符是一个单词的一部分。

`x-y`

:   A range of words; '`-y`'.

`*`


:   All of the words, except the `0` th. This is a synonym for '`1-$`' if there is just one word in the event; the empty string is returned in that case.

> 所有的单词，除了第0个以外。如果事件中只有一个单词，则这是“1-$”的同义词；在这种情况下，返回空字符串。

`x*`

:   Abbreviates '`x-$`'

`x-`

:   Abbreviates '`x-$`' is missing, it defaults to 0.


If a word designator is supplied without an event specification, the previous command is used as the event.

> 如果提供了单词指示器而没有指定事件，则会使用上一个命令作为事件。

---

::: header
Next: [Modifiers](Modifiers.html#Modifiers)]
:::
