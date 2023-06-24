---
tip: translate by openai@2023-06-23 19:14:29
...
---
description: Commands For Text (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Commands For Text (Debugging with GDB)
lang: en
resource-type: document
title: Commands For Text (Debugging with GDB)
---
::: header
Next: [Commands For Killing](Commands-For-Killing.html#Commands-For-Killing)]
:::

---

#### 33.4.3 Commands For Changing Text

`end-of-file (usually C-d)`


:   The character indicating end-of-file as set, for example, by `stty`. If this character is read when there are no characters on the line, and point is at the beginning of the line, Readline interprets it as the end of input and returns [EOF].

> 表示文件结束的字符，例如通过`stty`设置。如果在没有字符的情况下读取此字符，并且指针位于行首，Readline将其解释为输入结束，并返回[EOF]。

`delete-char (C-d)`


:   Delete the character at point. If this function is bound to the same character as the tty [EOF] commonly is, see above for the effects.

> 删除当前位置的字符。如果此函数绑定到与tty通常绑定的[EOF]相同的字符，请参阅上面的效果。

`backward-delete-char (Rubout)`


:   Delete the character behind the cursor. A numeric argument means to kill the characters instead of deleting them.

> 删除光标后面的字符。数字参数意味着将字符杀死而不是删除它们。

`forward-backward-delete-char ()`


:   Delete the character under the cursor, unless the cursor is at the end of the line, in which case the character behind the cursor is deleted. By default, this is not bound to a key.

> 删除光标下的字符，除非光标在行尾，在这种情况下，光标后的字符将被删除。默认情况下，此功能未绑定到任何键。

`quoted-insert (C-q or C-v)`


:   Add the next character typed to the line verbatim. This is how to insert key sequences like [C-q], for example.

> 把下一个输入的字符原样添加到行中。这就是如何插入像[C-q]这样的按键序列的方法。

`tab-insert (M-TAB)`

:   Insert a tab character.

`self-insert (a, b, A, 1, !, …)`

:   Insert yourself.

`bracketed-paste-begin ()`


:   This function is intended to be bound to the \"bracketed paste\" escape sequence sent by some terminals, and such a binding is assigned by default. It allows Readline to insert the pasted text as a single unit without treating each character as if it had been read from the keyboard. The characters are inserted as if each one was bound to `self-insert` instead of executing any editing commands.

> 这个功能旨在绑定到一些终端发送的"括号粘贴"转义序列，并且默认会分配这样一个绑定。它允许Readline以单个单元的形式插入粘贴的文本，而不是将每个字符都视为从键盘读取的。字符的插入方式就好像每个字符都绑定到`self-insert`而不是执行任何编辑命令。

```
Bracketed paste sets the region (the characters between point and the mark) to the inserted text. It uses the concept of an *active mark*: when the mark is active, Readline redisplay uses the terminal's standout mode to denote the region.
```

`transpose-chars (C-t)`


:   Drag the character before the cursor forward over the character at the cursor, moving the cursor forward as well. If the insertion point is at the end of the line, then this transposes the last two characters of the line. Negative arguments have no effect.

> 将光标前的字符拖动到光标处的字符上，同时将光标向前移动。如果插入点在行末，则会交换行末的最后两个字符。负参数无效。

`transpose-words (M-t)`


:   Drag the word before point past the word after point, moving point past that word as well. If the insertion point is at the end of the line, this transposes the last two words on the line.

> 将点前的单词拖动到点后的单词之后，并将点移到该单词之后。如果插入点在行末，则会将该行的最后两个单词互换。

`upcase-word (M-u)`


:   Uppercase the current (or following) word. With a negative argument, uppercase the previous word, but do not move the cursor.

> 大写当前（或者后面）的单词。使用负数参数，大写上一个单词，但不移动光标。

`downcase-word (M-l)`


:   Lowercase the current (or following) word. With a negative argument, lowercase the previous word, but do not move the cursor.

> 小写当前（或者后面）单词。使用负参数，小写上一个单词，但不移动光标。

`capitalize-word (M-c)`


:   Capitalize the current (or following) word. With a negative argument, capitalize the previous word, but do not move the cursor.

> 大写当前（或下一个）单词。如果有负参数，则大写上一个单词，但不移动光标。

`overwrite-mode ()`


:   Toggle overwrite mode. With an explicit positive numeric argument, switches to overwrite mode. With an explicit non-positive numeric argument, switches to insert mode. This command affects only `emacs` mode; `vi` mode does overwrite differently. Each call to `readline()` starts in insert mode.

> 切换覆盖模式。显式正数参数时，切换到覆盖模式。显式非正数参数时，切换到插入模式。此命令仅影响 `emacs` 模式；`vi` 模式的覆盖方式不同。每次调用 `readline()` 都从插入模式开始。

```
In overwrite mode, characters bound to `self-insert` replace the text at point rather than pushing the text to the right. Characters bound to `backward-delete-char` replace the character before point with a space.

By default, this command is unbound.
```

---

::: header
Next: [Commands For Killing](Commands-For-Killing.html#Commands-For-Killing)]
:::
