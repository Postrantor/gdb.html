---
description: Screen Size (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Screen Size (Debugging with GDB)
lang: en
resource-type: document
title: Screen Size (Debugging with GDB)
---
::: header
Next: [Output Styling](Output-Styling.html#Output-Styling)]
:::

---

### 22.4 Screen Size

Certain commands to [GDB] tries to break the line at a readable place, rather than simply letting it overflow onto the following line.

Normally [GDB] uses the termcap data base together with the value of the `TERM` environment variable and the `stty rows` and `stty cols` settings. If this is not correct, you can override it with the `set height` and `set width` commands:

`set height lpp`

`set height unlimited`

`show height`

`set width cpl`

`set width unlimited`

`show width`

These `set` commands specify a screen height of `lpp` characters. The associated `show` commands display the current settings.

If you specify a height of either `unlimited` or zero lines, [GDB] does not pause during output no matter how long the output is. This is useful if output is to a file or to an editor buffer.

Likewise, you can specify '`set width unlimited` from wrapping its output.

`set pagination on`

`set pagination off`

Turn the output pagination on or off; the default is on. Turning pagination off is the alternative to `set height unlimited`. Note that running [GDB] option (see [-batch](Mode-Options.html#Mode-Options)) also automatically disables pagination.

`show pagination`

Show the current pagination mode.

---

::: header
Next: [Output Styling](Output-Styling.html#Output-Styling)]
:::
