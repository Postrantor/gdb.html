---
tip: translate by openai@2023-06-24 00:25:36
...
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

> 读取`inputrc`文件的内容，并结合其中发现的任何绑定或变量赋值。

`abort (C-g)`


:   Abort the current editing command and ring the terminal's bell (subject to the setting of `bell-style`).

> 中止当前编辑命令，并根据`bell-style`的设置响铃终端。

`do-lowercase-version (M-A, M-B, M-x, …)`

:   If the metafied character `x` is already lower case.

`prefix-meta (ESC)`


:   Metafy the next character typed. This is for keyboards without a meta key. Typing '`ESC f`.

> 将下一个输入的字符元化。这是为没有Meta键的键盘准备的。输入' ESC f `。

`undo (C-_ or C-x C-u)`

:   Incremental undo, separately remembered for each line.

`revert-line (M-r)`


:   Undo all changes made to this line. This is like executing the `undo` command enough times to get back to the beginning.

> 撤消对此行所做的所有更改。这就像执行“撤消”命令足够次数以回到起点一样。

`tilde-expand (M-~)`

:   Perform tilde expansion on the current word.

`set-mark (C-@)`


:   Set the mark to the point. If a numeric argument is supplied, the mark is set to that position.

> 将标记设置为该点。如果提供了数字参数，则将标记设置为该位置。

`exchange-point-and-mark (C-x C-x)`


:   Swap the point with the mark. The current cursor position is set to the saved position, and the old cursor position is saved as the mark.

> 将点与标记互换。当前的光标位置设置为已保存的位置，而旧的光标位置被保存为标记。

`character-search (C-])`


:   A character is read and point is moved to the next occurrence of that character. A negative count searches for previous occurrences.

> 一个字符被读取，并且指针被移动到该字符的下一个出现的位置。负数搜索以前的出现。

`character-search-backward (M-C-])`


:   A character is read and point is moved to the previous occurrence of that character. A negative count searches for subsequent occurrences.

> 一个字符被读取，并且点被移动到该字符的上一次出现处。负数计数搜索后续出现。

`skip-csi-sequence ()`


:   Read enough characters to consume a multi-key sequence such as those defined for keys like Home and End. Such sequences begin with a Control Sequence Indicator (CSI), usually ESC-\[. If this sequence is bound to \"\\e\[\", keys producing such sequences will have no effect unless explicitly bound to a readline command, instead of inserting stray characters into the editing buffer. This is unbound by default, but usually bound to ESC-\[.

> 读取足够的字符以消耗像Home和End这样的键定义的多键序列。这些序列以控制序列指示符（CSI）开头，通常为ESC-\ [。如果将此序列绑定到“\ e \ [”，则产生此序列的键将不会起作用，除非明确将其绑定到readline命令，而不是将杂乱字符插入编辑缓冲区。默认情况下未绑定，但通常绑定到ESC-\ [。

`insert-comment (M-#)`


:   Without a numeric argument, the value of the `comment-begin` variable is inserted at the beginning of the current line. If a numeric argument is supplied, this command acts as a toggle: if the characters at the beginning of the line do not match the value of `comment-begin`, the value is inserted, otherwise the characters in `comment-begin` are deleted from the beginning of the line. In either case, the line is accepted as if a newline had been typed.

> 如果不提供数字参数，则将`comment-begin`变量的值插入到当前行的开头。如果提供数字参数，此命令充当切换：如果行开头的字符与`comment-begin`的值不匹配，则插入该值，否则从行开头删除`comment-begin`中的字符。无论哪种情况，都会接受该行，就像输入了新行一样。

`dump-functions ()`


:   Print all of the functions and their key bindings to the Readline output stream. If a numeric argument is supplied, the output is formatted in such a way that it can be made part of an `inputrc` file. This command is unbound by default.

> 打印所有函数及其键绑定到Readline输出流。如果提供了数字参数，则输出的格式可以成为`inputrc`文件的一部分。此命令默认未绑定。

`dump-variables ()`


:   Print all of the settable variables and their values to the Readline output stream. If a numeric argument is supplied, the output is formatted in such a way that it can be made part of an `inputrc` file. This command is unbound by default.

> 打印所有可设置的变量及其值到Readline输出流。如果提供了数字参数，则输出的格式可以成为`inputrc`文件的一部分。此命令默认未绑定。

`dump-macros ()`


:   Print all of the Readline key sequences bound to macros and the strings they output. If a numeric argument is supplied, the output is formatted in such a way that it can be made part of an `inputrc` file. This command is unbound by default.

> 打印所有绑定到宏的Readline键序列及其输出的字符串。如果提供了数值参数，则输出的格式可以成为`inputrc`文件的一部分。默认情况下，此命令未绑定。

`emacs-editing-mode (C-e)`


:   When in `vi` command mode, this causes a switch to `emacs` editing mode.

> 当在vi命令模式下，这会导致切换到emacs编辑模式。

`vi-editing-mode (M-C-j)`


:   When in `emacs` editing mode, this causes a switch to `vi` editing mode.

> 当处于Emacs编辑模式时，这会导致切换到Vi编辑模式。

---

::: header
Previous: [Keyboard Macros](Keyboard-Macros.html#Keyboard-Macros)]
:::
