---
tip: translate by openai@2023-06-23 20:52:48
...
---
description: Event Designators (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Event Designators (Debugging with GDB)
lang: en
resource-type: document
title: Event Designators (Debugging with GDB)
---
::: header
Next: [Word Designators](Word-Designators.html#Word-Designators)]
:::

---

#### 34.1.1 Event Designators


An event designator is a reference to a command line entry in the history list. Unless the reference is absolute, events are relative to the current position in the history list.

> 事件设计器是对历史列表中命令行条目的引用。除非引用是绝对的，否则事件相对于历史列表中的当前位置。

`!`


:   Start a history substitution, except when followed by a space, tab, the end of the line, or '`=`'.

> 开始历史替换，除非后面跟着空格、制表符、行末或'`='`。

`!n`

:   Refer to command line `n`.

`!-n`

:   Refer to the command `n` lines back.

`!!`

:   Refer to the previous command. This is a synonym for '`!-1`'.

`!string`


:   Refer to the most recent command preceding the current position in the history list starting with `string`.

> 参考从`字符串`开始的历史列表中当前位置之前的最新命令。

`!?string[?]`


:   Refer to the most recent command preceding the current position in the history list containing `string` is missing, the string from the most recent search is used; it is an error if there is no previous search string.

> 如果在历史列表中当前位置之前没有最近的命令包含`string`，则使用最近搜索的字符串；如果没有先前的搜索字符串，则会出错。

`^string1^string2^`


:   Quick Substitution. Repeat the last command, replacing `string1`. Equivalent to `!!:s^string1^string2^`.

> 快速替换。重复上一个命令，替换`string1`。等价于`!!:s ^ string1 ^ string2 ^`。

`!#`

:   The entire command line typed so far.
