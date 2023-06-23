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

`previous-history (C-p)`

:   Move 'back' through the history list, fetching the previous command.

`next-history (C-n)`

:   Move 'forward' through the history list, fetching the next command.

`beginning-of-history (M-<)`

:   Move to the first line in the history.

`end-of-history (M->)`

:   Move to the end of the input history, i.e., the line currently being entered.

`reverse-search-history (C-r)`

:   Search backward starting at the current line and moving 'up' through the history as necessary. This is an incremental search. This command sets the region to the matched text and activates the mark.

`forward-search-history (C-s)`

:   Search forward starting at the current line and moving 'down' through the history as necessary. This is an incremental search. This command sets the region to the matched text and activates the mark.

`non-incremental-reverse-search-history (M-p)`

:   Search backward starting at the current line and moving 'up' through the history as necessary using a non-incremental search for a string supplied by the user. The search string may match anywhere in a history line.

`non-incremental-forward-search-history (M-n)`

:   Search forward starting at the current line and moving 'down' through the history as necessary using a non-incremental search for a string supplied by the user. The search string may match anywhere in a history line.

`history-search-forward ()`

:   Search forward through the history for the string of characters between the start of the current line and the point. The search string must match at the beginning of a history line. This is a non-incremental search. By default, this command is unbound.

`history-search-backward ()`

:   Search backward through the history for the string of characters between the start of the current line and the point. The search string must match at the beginning of a history line. This is a non-incremental search. By default, this command is unbound.

`history-substring-search-forward ()`

:   Search forward through the history for the string of characters between the start of the current line and the point. The search string may match anywhere in a history line. This is a non-incremental search. By default, this command is unbound.

`history-substring-search-backward ()`

:   Search backward through the history for the string of characters between the start of the current line and the point. The search string may match anywhere in a history line. This is a non-incremental search. By default, this command is unbound.

`yank-nth-arg (M-C-y)`

:   Insert the first argument to the previous command (usually the second word on the previous line) at point. With an argument `n`' history expansion had been specified.

`yank-last-arg (M-. or M-_)`

:   Insert last argument to the previous command (the last word of the previous history entry). With a numeric argument, behave exactly like `yank-nth-arg`. Successive calls to `yank-last-arg` move back through the history list, inserting the last word (or the word specified by the argument to the first call) of each line in turn. Any numeric argument supplied to these successive calls determines the direction to move through the history. A negative argument switches the direction through the history (back or forward). The history expansion facilities are used to extract the last argument, as if the '`!$`' history expansion had been specified.

`operate-and-get-next (C-o)`

:   Accept the current line for return to the calling application as if a newline had been entered, and fetch the next line relative to the current line from the history for editing. A numeric argument, if supplied, specifies the history entry to use instead of the current line.

---

::: header
Next: [Commands For Text](Commands-For-Text.html#Commands-For-Text)]
:::
