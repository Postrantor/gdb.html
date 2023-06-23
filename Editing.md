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

You may control the behavior of command line editing in [GDB] with the command `set`.

`set editing`

`set editing on`

Enable command line editing (enabled by default).

`set editing off`

Disable command line editing.

`show editing`

Show whether command line editing is enabled.

See [Command Line Editing](Command-Line-Editing.html#Command-Line-Editing), for more details about the Readline interface. Users unfamiliar with [GNU] Emacs or `vi` are encouraged to read that chapter.

[GDB].

[GDB] by default. This command accepts the current line for execution and fetches the next line relative to the current line from the history for editing. Any argument is ignored.
