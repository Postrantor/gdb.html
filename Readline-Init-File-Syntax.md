---
tip: translate by openai@2023-06-24 01:52:55
...
---
description: Readline Init File Syntax (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Readline Init File Syntax (Debugging with GDB)
lang: en
resource-type: document
title: Readline Init File Syntax (Debugging with GDB)
---
::: header
Next: [Conditional Init Constructs](Conditional-Init-Constructs.html#Conditional-Init-Constructs)]
:::

---

#### 33.3.1 Readline Init File Syntax


There are only a few basic constructs allowed in the Readline init file. Blank lines are ignored. Lines beginning with a '`#`' indicate conditional constructs (see [Conditional Init Constructs](Conditional-Init-Constructs.html#Conditional-Init-Constructs)). Other lines denote variable settings and key bindings.

> 只允许在Readline初始文件中使用几个基本结构。空行将被忽略。以'#'开头的行表示条件结构（参见[条件初始结构]（Conditional-Init-Constructs.html#Conditional-Init-Constructs））。其他行表示变量设置和按键绑定。

Variable Settings


:   You can modify the run-time behavior of Readline by altering the values of variables in Readline using the `set` command within the init file. The syntax is simple:

> 你可以通过在init文件中使用'set'命令更改Readline的运行时行为。语法很简单：

```
::: example
``` example
set variable value
```

:::

Here, for example, is how to change from the default Emacs-like key binding to use `vi` line editing commands:

::: example

```example
set editing-mode vi
```

:::

Variable names and values, where appropriate, are recognized without regard to case. Unrecognized variable names are ignored.

Boolean variables (those that can be set to on or off) are set to on if the value is null or empty, `on` (case-insensitive), or 1. Any other value results in the variable being set to off.

A great deal of run-time behavior is changeable with the following variables.

`bell-style`

:

```

Controls what happens when Readline wants to ring the terminal bell. If set to '`none`' (the default), Readline attempts to ring the terminal's bell.

> 当Readline想要响铃时，控制发生什么。如果设置为“none”（默认值），Readline会尝试响铃终端的铃声。
```

`bind-tty-special-chars`

:

```

If set to '`on`' (the default), Readline attempts to bind the control characters treated specially by the kernel's terminal driver to their Readline equivalents.

> 如果设置为“开启”（默认值），Readline会尝试将内核终端驱动程序特殊处理的控制字符绑定到其Readline等效物。
```

`blink-matching-paren`

:

```
If set to '`on`'.
```

`colored-completion-prefix`

:

```
If set to '`on`'.
```

`colored-stats`

:

```
If set to '`on`'.
```

`comment-begin`

:

```

The string to insert at the beginning of the line when the `insert-comment` command is executed. The default value is `"#"`.

> 当执行`insert-comment`命令时，在行首插入的字符串，默认值为`"#"`。
```

`completion-display-width`

:

```

The number of screen columns used to display possible matches when performing completion. The value is ignored if it is less than 0 or greater than the terminal screen width. A value of 0 will cause matches to be displayed one per line. The default value is -1.

> 用于显示可能匹配项时使用的屏幕列数。如果值小于0或大于终端屏幕宽度，则忽略此值。值为0时，将每行显示一个匹配项。默认值为-1。
```

`completion-ignore-case`

:

```
If set to '`on`'.
```

`completion-map-case`

:

```
If set to '`on`'.
```

`completion-prefix-display-length`

:

```

The length in characters of the common prefix of a list of possible completions that is displayed without modification. When set to a value greater than zero, common prefixes longer than this value are replaced with an ellipsis when displaying possible completions.

> 列出可能补全的列表的公共前缀的字符长度，在设置为大于零的值时，在显示可能补全时，公共前缀超过此值的部分将被省略号替换。
```

`completion-query-items`

:

```

The number of possible completions that determines when the user is asked whether the list of possibilities should be displayed. If the number of possible completions is greater than or equal to this value, Readline will ask whether or not the user wishes to view them; otherwise, they are simply listed. This variable must be set to an integer value greater than or equal to 0. A negative value means Readline should never ask. The default limit is `100`.

> 当用户被问及是否需要显示可能完成的列表时，决定可能完成的数量。如果可能完成的数量大于或等于这个值，Readline将询问用户是否需要查看它们；否则，它们将被简单地列出。此变量必须设置为大于或等于0的整数值。负值表示Readline永远不会问。默认限制为`100`。
```

`convert-meta`

:

```
If set to '`on`' if the locale is one that contains eight-bit characters.
```

`disable-completion`

:

```
If set to '`On`'.
```

`echo-control-characters`

:

```
When set to '`on`'.
```

`editing-mode`

:

```

The `editing-mode` variable controls which default set of key bindings is used. By default, Readline starts up in Emacs editing mode, where the keystrokes are most similar to Emacs. This variable can be set to either '`emacs`'.

> 变量`editing-mode`控制使用哪组默认的键绑定。默认情况下，Readline以Emacs编辑模式启动，其键击最接近Emacs。该变量可以设置为'`emacs`'。
```

`emacs-mode-string`

:

```
If the `show-mode-in-prompt`'.
```

`enable-bracketed-paste`

:

```
When set to '`On`'.
```

`enable-keypad`

:

```
When set to '`on`'.
```

`enable-meta-key`

:   When set to '`on`'.

`expand-tilde`

:

```
If set to '`on`'.
```

`history-preserve-point`

:

```
If set to '`on`'.
```

`history-size`

:

```

Set the maximum number of history entries saved in the history list. If set to zero, any existing history entries are deleted and no new entries are saved. If set to a value less than zero, the number of history entries is not limited. By default, the number of history entries is not limited. If an attempt is made to set `history-size` to a non-numeric value, the maximum number of history entries will be set to 500.

> 设置历史记录列表中保存的最大历史记录条目数。如果设置为零，则删除任何现有的历史记录，不保存新的记录。如果设置为小于零的值，则不限制历史记录条目数。默认情况下，不限制历史记录条目数。如果试图将“history-size”设置为非数字值，则将最大历史记录条目数设置为500。
```

`horizontal-scroll-mode`

:

```
This variable can be set to either '`on`'.
```

`input-meta`

:

```

If set to '`on`' if the locale contains eight-bit characters. The name `meta-flag` is a synonym for this variable.

> 如果设置为“on”，如果语言环境包含八位字符，则将meta-flag变量同义词。
```

`isearch-terminators`

:

```

The string of characters that should terminate an incremental search without subsequently executing the character as a command (see [Searching](Searching.html#Searching)). If this variable has not been given a value, the characters ESC and [C-J] will terminate an incremental search.

> 如果没有给出值，ESC和[C-J]将终止增量搜索，这个变量应该用来结束增量搜索而不会执行该字符作为命令（参见[搜索](Searching.html#Searching)）。
```

`keymap`

:

```

Sets Readline's idea of the current keymap for key binding commands. Built-in `keymap` names are `emacs`, `emacs-standard`, `emacs-meta`, `emacs-ctlx`, `vi`, `vi-move`, `vi-command`, and `vi-insert`. `vi` is equivalent to `vi-command` (`vi-move` is also a synonym); `emacs` is equivalent to `emacs-standard`. Applications may add additional names. The default value is `emacs`. The value of the `editing-mode` variable also affects the default keymap.

> 设置Readline的当前键绑定命令的键映射想法。内置的`keymap`名称有`emacs`、`emacs-standard`、`emacs-meta`、`emacs-ctlx`、`vi`、`vi-move`、`vi-command`和`vi-insert`。`vi`等同于`vi-command`（`vi-move`也是同义词）；`emacs`等同于`emacs-standard`。应用程序可以添加其他名称。默认值为`emacs`。`editing-mode`变量的值也会影响默认的键映射。
```

`keyseq-timeout`

:   Specifies the duration Readline will wait for a character when reading an ambiguous key sequence (one that can form a complete key sequence using the input read so far, or can take additional input to complete a longer key sequence). If no input is received within the timeout, Readline will use the shorter but complete key sequence. Readline uses this value to determine whether or not input is available on the current input source (`rl_instream` by default). The value is specified in milliseconds, so a value of 1000 means that Readline will wait one second for additional input. If this variable is set to a value less than or equal to zero, or to a non-numeric value, Readline will wait until another key is pressed to decide which key sequence to complete. The default value is `500`.

`mark-directories`

:   If set to '`on`'.

`mark-modified-lines`

:

```
This variable, when set to '`on`' by default.
```

`mark-symlinked-directories`

:

```
If set to '`on`'.
```

`match-hidden-files`

:

```
This variable, when set to '`on`' by default.
```

`menu-complete-display-prefix`

:

```
If set to '`on`'.
```

`output-meta`

:

```
If set to '`on`' if the locale contains eight-bit characters.
```

`page-completions`

:

```
If set to '`on`' by default.
```

`print-completions-horizontally`

:   If set to '`on`'.

`revert-all-at-newline`

:

```
If set to '`on`'.
```

`show-all-if-ambiguous`

:

```

This alters the default behavior of the completion functions. If set to '`on`'.

> 这会改变补全功能的默认行为。如果设置为“on”。
```

`show-all-if-unmodified`

:

```

This alters the default behavior of the completion functions in a fashion similar to `show-all-if-ambiguous`'.

> 这改变了完成函数的默认行为，类似于`show-all-if-ambiguous`。
```

`show-mode-in-prompt`

:

```
If set to '`on`'.
```

`skip-completed-text`

:

```
If set to '`on`'.
```

`vi-cmd-mode-string`

:

```
If the `show-mode-in-prompt`'.
```

`vi-ins-mode-string`

:

```
If the `show-mode-in-prompt`'.
```

`visible-stats`

:

```
If set to '`on`'.
```

```

Key Bindings


:   The syntax for controlling key bindings in the init file is simple. First you need to find the name of the command that you want to change. The following sections contain tables of the command name, the default keybinding, if any, and a short description of what the command does.

> 在初始文件中控制键绑定的语法很简单。首先，您需要找到要更改的命令的名称。以下部分包含命令名称、默认键绑定（如果有）以及命令功能的短说明的表格。

```

Once you know the name of the command, simply place on a line in the init file the name of the key you wish to bind the command to, a colon, and then the name of the command. There can be no space between the key name and the colon -- that will be interpreted as part of the key name. The name of the key can be expressed in different ways, depending on what you find most comfortable.

In addition to command names, readline allows keys to be bound to a string that is inserted when the key is pressed (a `macro`).

`keyname`

:   `keyname` is the name of a key spelled out in English. For example:

```
::: example
``` example
Control-u: universal-argument
Meta-Rubout: backward-kill-word
Control-o: "> output"
```

:::

In the example above, [C-u]' into the line).


A number of symbolic character names are recognized while processing this key binding syntax: `DEL`.

> 在处理这个键绑定语法时，会识别出一些符号性的字符名称：DEL。

```

\"`keyseq`

:   `keyseq` Emacs style key escapes can be used, as in the following example, but the special character names are not recognized.

```

::: example

```example
"\C-u": universal-argument
"\C-x\C-r": re-read-init-file
"\e[11~": "Function Key 1"
```

:::

In the above example, [C-u]'.

```

The following [GNU] Emacs style escape sequences are available when specifying key sequences:

`\C-`

:   control prefix

`\M-`

:   meta prefix

`\e`

:   an escape character

`\\`

:   backslash

`\"`

:   \", a double quotation mark

`\'`

:   \', a single quote or apostrophe

In addition to the [GNU] Emacs style escape sequences, a second set of backslash escapes is available:

`\a`

:   alert (bell)

`\b`

:   backspace

`\d`

:   delete

`\f`

:   form feed

`\n`

:   newline

`\r`

:   carriage return

`\t`

:   horizontal tab

`\v`

:   vertical tab

`\nnn`

:   the eight-bit character whose value is the octal value `nnn` (one to three digits)

`\xHH`

:   the eight-bit character whose value is the hexadecimal value `HH` (one or two hex digits)

When entering the text of a macro, single or double quotes must be used to indicate a macro definition. Unquoted text is assumed to be a function name. In the macro body, the backslash escapes described above are expanded. Backslash will quote any other character in the macro text, including '`"`' into the line:

::: example

```example
"\C-x\\": "\\"
```

:::

```

---

::: header
Next: [Conditional Init Constructs](Conditional-Init-Constructs.html#Conditional-Init-Constructs)]
:::
```
