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

[GDB] command names may always be truncated if that abbreviation is unambiguous. Other possible command abbreviations are listed in the documentation for individual commands. In some cases, even ambiguous abbreviations are allowed; for example, `s` is specially defined as equivalent to `step` even though there are other commands whose names start with `s`. You can test abbreviations by using them as arguments to the `help` command.

A blank line as input to [GDB] (typing just RET) means to repeat the previous command. Certain commands (for example, `run`) will not repeat this way; these are commands whose unintentional repetition might cause trouble and which you are unlikely to want to repeat. User-defined commands can disable this feature; see [dont-repeat](Define.html#Define).

The `list` and `x` commands, when you repeat them with RET, construct new arguments rather than repeating exactly as typed. This permits easy scanning of source or memory.

[GDB] disables command repetition after any command that generates this sort of display.

Any text from a [\#] to the end of the line is a comment; it does nothing. This is useful mainly in command files (see [Command Files](Command-Files.html#Command-Files)).

The [Ctrl-o] binding is useful for repeating a complex sequence of commands. This command accepts the current line, like RET, and then fetches the next line relative to the current line from the history for editing.

---

::: header
Next: [Command Settings](Command-Settings.html#Command-Settings)]
:::
