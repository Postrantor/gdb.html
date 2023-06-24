---
tip: translate by openai@2023-06-23 20:46:14
...
---
description: Editing (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Editing (Debugging with GDB)
lang: en
resource-type: document
title: Editing (Debugging with GDB)
---
::: header
Next: [Command History](Command-History.html#Command-History)]
:::

---

### 22.2 Command Editing


[GDB] Emacs-style or *vi*-style inline editing of commands, `csh`-like history substitution, and a storage and recall of command history across debugging sessions.

> GDB 支持 Emacs 风格或 vi 风格的内联命令编辑、类似 csh 的历史替换以及调试会话间的命令历史存储和检索。


You may control the behavior of command line editing in [GDB] with the command `set`.

> 你可以使用命令`set`来控制[GDB]中命令行编辑的行为。

`set editing`

`set editing on`

Enable command line editing (enabled by default).

`set editing off`

Disable command line editing.

`show editing`

Show whether command line editing is enabled.


See [Command Line Editing](Command-Line-Editing.html#Command-Line-Editing), for more details about the Readline interface. Users unfamiliar with [GNU] Emacs or `vi` are encouraged to read that chapter.

> 请参阅[命令行编辑](Command-Line-Editing.html#Command-Line-Editing)，以了解更多有关Readline界面的详细信息。鼓励不熟悉[GNU] Emacs或`vi`的用户阅读该章节。

[GDB].


[GDB] by default. This command accepts the current line for execution and fetches the next line relative to the current line from the history for editing. Any argument is ignored.

> 默认情况下，此命令会接受当前行的执行，并从历史记录中获取相对于当前行的下一行进行编辑。任何参数都会被忽略。
