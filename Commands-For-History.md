---
tip: translate by openai@2023-06-23 19:10:42
...
---
description: Commands For History (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Commands For History (Debugging with GDB)
lang: en
resource-type: document
title: Commands For History (Debugging with GDB)
---
::: header
Next: [Commands For Text](Commands-For-Text.html#Commands-For-Text)]
:::

---

#### 33.4.2 Commands For Manipulating The History

`accept-line (Newline or Return)`


:   Accept the line regardless of where the cursor is. If this line is non-empty, it may be added to the history list for future recall with `add_history()`. If this line is a modified history line, the history line is restored to its original state.

> 不管光标在哪里，都接受这一行。如果这一行不为空，可以使用`add_history()`将它添加到历史记录列表中以供将来查询。如果这一行是修改过的历史行，则将该历史行恢复到原始状态。

`previous-history (C-p)`

:   Move 'back' through the history list, fetching the previous command.

`next-history (C-n)`

:   Move 'forward' through the history list, fetching the next command.

`beginning-of-history (M-<)`

:   Move to the first line in the history.

`end-of-history (M->)`


:   Move to the end of the input history, i.e., the line currently being entered.

> 移动到输入历史的末尾，即当前正在输入的行。

`reverse-search-history (C-r)`


:   Search backward starting at the current line and moving 'up' through the history as necessary. This is an incremental search. This command sets the region to the matched text and activates the mark.

> 从当前行开始向上搜索历史记录，如有必要。这是一个增量搜索。此命令将区域设置为匹配的文本，并激活标记。

`forward-search-history (C-s)`


:   Search forward starting at the current line and moving 'down' through the history as necessary. This is an incremental search. This command sets the region to the matched text and activates the mark.

> 从当前行开始向下搜索，如有必要，可移动到历史记录中。这是一个增量搜索。此命令将区域设置为匹配的文本，并激活标记。

`non-incremental-reverse-search-history (M-p)`


:   Search backward starting at the current line and moving 'up' through the history as necessary using a non-incremental search for a string supplied by the user. The search string may match anywhere in a history line.

> 从当前行开始向上搜索历史记录，根据用户提供的字符串进行非增量搜索。搜索字符串可以在历史行中的任何位置匹配。

`non-incremental-forward-search-history (M-n)`


:   Search forward starting at the current line and moving 'down' through the history as necessary using a non-incremental search for a string supplied by the user. The search string may match anywhere in a history line.

> 从当前行开始向下搜索，必要时通过非增量搜索搜索用户提供的字符串。搜索字符串可以匹配历史行中的任何位置。

`history-search-forward ()`


:   Search forward through the history for the string of characters between the start of the current line and the point. The search string must match at the beginning of a history line. This is a non-incremental search. By default, this command is unbound.

> 搜索当前行开头到当前位置之间的字符串。搜索字符串必须匹配历史行的开头。这是一个非增量搜索。默认情况下，此命令未绑定。

`history-search-backward ()`


:   Search backward through the history for the string of characters between the start of the current line and the point. The search string must match at the beginning of a history line. This is a non-incremental search. By default, this command is unbound.

> 搜索历史记录，以查找从当前行开始到光标位置的字符串。搜索字符串必须在历史行的开头匹配。这是一个非增量搜索。默认情况下，此命令未绑定。

`history-substring-search-forward ()`


:   Search forward through the history for the string of characters between the start of the current line and the point. The search string may match anywhere in a history line. This is a non-incremental search. By default, this command is unbound.

> 搜索当前行起始点到光标位置之间的字符串。搜索字符串可以匹配历史行中的任何位置。这是一个非增量搜索。默认情况下，此命令未绑定。

`history-substring-search-backward ()`


:   Search backward through the history for the string of characters between the start of the current line and the point. The search string may match anywhere in a history line. This is a non-incremental search. By default, this command is unbound.

> 搜索历史记录，以查找从当前行开头到当前位置之间的字符串。搜索字符串可以在历史行中的任何位置匹配。这是一个非增量搜索。默认情况下，此命令未绑定。

`yank-nth-arg (M-C-y)`


:   Insert the first argument to the previous command (usually the second word on the previous line) at point. With an argument `n`' history expansion had been specified.

> 插入上一个命令的第一个参数（通常是上一行的第二个单词）到当前位置。如果指定了参数`n`，则进行历史展开。

`yank-last-arg (M-. or M-_)`


:   Insert last argument to the previous command (the last word of the previous history entry). With a numeric argument, behave exactly like `yank-nth-arg`. Successive calls to `yank-last-arg` move back through the history list, inserting the last word (or the word specified by the argument to the first call) of each line in turn. Any numeric argument supplied to these successive calls determines the direction to move through the history. A negative argument switches the direction through the history (back or forward). The history expansion facilities are used to extract the last argument, as if the '`!$`' history expansion had been specified.

> 将上一条命令的最后一个参数插入到前一条命令中（前一条历史记录的最后一个单词）。带有数字参数时，行为与`yank-nth-arg`完全相同。连续调用`yank-last-arg`会依次向后移动历史列表，插入每行的最后一个单词（或第一次调用时指定的单词）。这些连续调用提供的任何数字参数都会确定移动历史的方向。负参数会切换历史的方向（向后或向前）。使用历史展开功能来提取最后一个参数，就好像指定了'`!$`'历史展开一样。

`operate-and-get-next (C-o)`


:   Accept the current line for return to the calling application as if a newline had been entered, and fetch the next line relative to the current line from the history for editing. A numeric argument, if supplied, specifies the history entry to use instead of the current line.

> 接受当前行作为返回至调用应用的结果，就像输入了一个新行一样，并从历史记录中获取与当前行相关的下一行进行编辑。如果提供了数值参数，则指定使用历史记录条目而不是当前行。

---

::: header
Next: [Commands For Text](Commands-For-Text.html#Commands-For-Text)]
:::
