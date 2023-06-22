---
description: TUI Single Key Mode (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: TUI Single Key Mode (Debugging with GDB)
lang: en
resource-type: document
title: TUI Single Key Mode (Debugging with GDB)
---
::: header
Next: [TUI Mouse Support](TUI-Mouse-Support.html#TUI-Mouse-Support)]
:::

---

### 25.3 TUI Single Key Mode

The TUI also provides a *SingleKey* mode, which binds several frequently used [GDB] to switch into this mode, where the following key bindings are used:

[c]

continue

[d]

down

[f]

finish

[n]

next

[o]

nexti. The shortcut letter '`o`' stands for "step Over".

[q]

exit the SingleKey mode.

[r]

run

[s]

step

[i]

stepi. The shortcut letter '`i`' stands for "step Into".

[u]

up

[v]

info locals

[w]

where

Other keys temporarily switch to the [GDB].

If [GDB] to add additional bindings to this keymap.
