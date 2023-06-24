---
tip: translate by openai@2023-06-23 19:09:08
...
---
description: Command Syntax (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Command Syntax (Debugging with GDB)
lang: en
resource-type: document
title: Command Syntax (Debugging with GDB)
---
::: header
Next: [Command Settings](Command-Settings.html#Command-Settings)]
:::

---

### 3.1 Command Syntax


A [GDB]'. You can also use the `step` command with no arguments. Some commands do not allow any arguments.

> 一个[GDB]。您也可以使用不带任何参数的`step`命令。有些命令不允许任何参数。


[GDB] command names may always be truncated if that abbreviation is unambiguous. Other possible command abbreviations are listed in the documentation for individual commands. In some cases, even ambiguous abbreviations are allowed; for example, `s` is specially defined as equivalent to `step` even though there are other commands whose names start with `s`. You can test abbreviations by using them as arguments to the `help` command.

> GDB 命令名称可以简写，只要简写是不模糊的。其他可能的命令缩写在每个命令的文档中有列出。在某些情况下，即使是模糊的缩写也是允许的；例如，“s” 被特殊定义为等同于“step”，即使有其他命令的名称以“s”开头。您可以通过将缩写作为“help”命令的参数来测试缩写。


A blank line as input to [GDB] (typing just RET) means to repeat the previous command. Certain commands (for example, `run`) will not repeat this way; these are commands whose unintentional repetition might cause trouble and which you are unlikely to want to repeat. User-defined commands can disable this feature; see [dont-repeat](Define.html#Define).

> 输入空行到GDB（只键入RET）意味着重复上一个命令。某些命令（例如“run”）无法重复，这些命令的无意重复可能会造成麻烦，而且你不太可能想重复它们。用户定义的命令可以禁用此功能；请参见dont-repeat。


The `list` and `x` commands, when you repeat them with RET, construct new arguments rather than repeating exactly as typed. This permits easy scanning of source or memory.

> 列表和X命令，当你用RET重复它们时，会构造新的参数而不是确切地重复所输入的内容。这样可以方便地扫描源代码或内存。


[GDB] disables command repetition after any command that generates this sort of display.

> [GDB] 在生成此类显示之后禁用命令重复。


Any text from a [\#] to the end of the line is a comment; it does nothing. This is useful mainly in command files (see [Command Files](Command-Files.html#Command-Files)).

> 从[#]开始到行尾的任何文本都是注释；它什么也不做。这主要在命令文件中很有用（参见[命令文件](Command-Files.html#Command-Files)）。


The [Ctrl-o] binding is useful for repeating a complex sequence of commands. This command accepts the current line, like RET, and then fetches the next line relative to the current line from the history for editing.

> 绑定[Ctrl-o]很有用，用于重复一系列复杂的命令。这个命令像RET一样接受当前行，然后从历史记录中获取相对于当前行的下一行进行编辑。

---

::: header
Next: [Command Settings](Command-Settings.html#Command-Settings)]
:::
