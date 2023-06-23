---
description: Miscellaneous Commands (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Miscellaneous Commands (Debugging with GDB)
lang: en
resource-type: document
title: Miscellaneous Commands (Debugging with GDB)
---
::: header
Previous: [Keyboard Macros](Keyboard-Macros.html#Keyboard-Macros)]
:::

---

#### 33.4.8 Some Miscellaneous Commands

`re-read-init-file (C-x C-r)`

:   Read in the contents of the `inputrc` file, and incorporate any bindings or variable assignments found there.

`abort (C-g)`

:   Abort the current editing command and ring the terminal's bell (subject to the setting of `bell-style`).

`do-lowercase-version (M-A, M-B, M-x, …)`

:   If the metafied character `x` is already lower case.

`prefix-meta (ESC)`

:   Metafy the next character typed. This is for keyboards without a meta key. Typing '`ESC f`.

`undo (C-_ or C-x C-u)`

:   Incremental undo, separately remembered for each line.

`revert-line (M-r)`

:   Undo all changes made to this line. This is like executing the `undo` command enough times to get back to the beginning.

`tilde-expand (M-~)`

:   Perform tilde expansion on the current word.

`set-mark (C-@)`

:   Set the mark to the point. If a numeric argument is supplied, the mark is set to that position.

`exchange-point-and-mark (C-x C-x)`

:   Swap the point with the mark. The current cursor position is set to the saved position, and the old cursor position is saved as the mark.

`character-search (C-])`

:   A character is read and point is moved to the next occurrence of that character. A negative count searches for previous occurrences.

`character-search-backward (M-C-])`

:   A character is read and point is moved to the previous occurrence of that character. A negative count searches for subsequent occurrences.

`skip-csi-sequence ()`

:   Read enough characters to consume a multi-key sequence such as those defined for keys like Home and End. Such sequences begin with a Control Sequence Indicator (CSI), usually ESC-\[. If this sequence is bound to \"\\e\[\", keys producing such sequences will have no effect unless explicitly bound to a readline command, instead of inserting stray characters into the editing buffer. This is unbound by default, but usually bound to ESC-\[.

`insert-comment (M-#)`

:   Without a numeric argument, the value of the `comment-begin` variable is inserted at the beginning of the current line. If a numeric argument is supplied, this command acts as a toggle: if the characters at the beginning of the line do not match the value of `comment-begin`, the value is inserted, otherwise the characters in `comment-begin` are deleted from the beginning of the line. In either case, the line is accepted as if a newline had been typed.

`dump-functions ()`

:   Print all of the functions and their key bindings to the Readline output stream. If a numeric argument is supplied, the output is formatted in such a way that it can be made part of an `inputrc` file. This command is unbound by default.

`dump-variables ()`

:   Print all of the settable variables and their values to the Readline output stream. If a numeric argument is supplied, the output is formatted in such a way that it can be made part of an `inputrc` file. This command is unbound by default.

`dump-macros ()`

:   Print all of the Readline key sequences bound to macros and the strings they output. If a numeric argument is supplied, the output is formatted in such a way that it can be made part of an `inputrc` file. This command is unbound by default.

`emacs-editing-mode (C-e)`

:   When in `vi` command mode, this causes a switch to `emacs` editing mode.

`vi-editing-mode (M-C-j)`

:   When in `emacs` editing mode, this causes a switch to `vi` editing mode.

---

::: header
Previous: [Keyboard Macros](Keyboard-Macros.html#Keyboard-Macros)]
:::
