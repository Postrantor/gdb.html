---
tip: translate by openai@2023-06-24 02:20:13
...
---
description: Searching (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Searching (Debugging with GDB)
lang: en
resource-type: document
title: Searching (Debugging with GDB)
---
::: header
Previous: [Readline Arguments](Readline-Arguments.html#Readline-Arguments)]
:::

---

#### 33.2.5 Searching for Commands in the History


Readline provides commands for searching through the command history for lines containing a specified string. There are two search modes: *incremental* and *non-incremental*.

> Readline提供命令来搜索包含指定字符串的命令历史记录。有两种搜索模式：*增量*和*非增量*。


Incremental searches begin before the user has finished typing the search string. As each character of the search string is typed, Readline displays the next entry from the history matching the string typed so far. An incremental search requires only as many characters as needed to find the desired history entry. To search backward in the history for a particular string, type [C-r] will abort an incremental search and restore the original line. When the search is terminated, the history entry containing the search string becomes the current line.

> 随着用户输入搜索字符串的每个字符，Readline会显示与已输入字符串匹配的历史记录的下一条记录。增量搜索只需要输入足够的字符来找到所需的历史记录。要向后搜索历史记录中的特定字符串，请键入[C-r]，将中止增量搜索并恢复原始行。当搜索终止时，包含搜索字符串的历史记录成为当前行。


To find other matching entries in the history list, type [C-r] as appropriate. This will search backward or forward in the history for the next entry matching the search string typed so far. Any other key sequence bound to a Readline command will terminate the search and execute that command. For instance, a RET will terminate the search and accept the line, thereby executing the command from the history list. A movement command will terminate the search, make the last line found the current line, and begin editing.

> 要在历史列表中查找其他匹配的条目，按[C-r]，根据情况而定。这将在历史记录中向前或向后搜索与到目前为止输入的搜索字符串匹配的下一个条目。任何其他绑定到Readline命令的键序列都将终止搜索并执行该命令。例如，RET将终止搜索并接受该行，从而执行历史列表中的命令。移动命令将终止搜索，使最后一行成为当前行，并开始编辑。


Readline remembers the last incremental search string. If two [C-r]s are typed without any intervening characters defining a new search string, any remembered search string is used.

> 当输入两次[C-r]，而中间没有定义新的搜索字符串时，Readline会记住上一次的增量搜索字符串。


Non-incremental searches read the entire search string before starting to search for matching history lines. The search string may be typed by the user or be part of the contents of the current line.

> 非增量搜索在开始搜索匹配的历史行之前会先读取整个搜索字符串。搜索字符串可以是用户输入的，也可以是当前行的内容的一部分。

---

::: header
Previous: [Readline Arguments](Readline-Arguments.html#Readline-Arguments)]
:::
