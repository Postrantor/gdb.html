---
description: TUI Keys (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: TUI Keys (Debugging with GDB)
lang: en
resource-type: document
title: TUI Keys (Debugging with GDB)
---
::: header
Next: [TUI Single Key Mode](TUI-Single-Key-Mode.html#TUI-Single-Key-Mode)]
:::

---

### 25.2 TUI Key Bindings

The TUI installs several key bindings in the readline keymaps (see [Command Line Editing](Command-Line-Editing.html#Command-Line-Editing)). The following key bindings are installed for both TUI mode and the [GDB] standard mode.

[C-x C-a]

[C-x a]

[C-x A]

Enter or leave the TUI mode. When leaving the TUI mode, the curses window management stops and [GDB] operates using its standard mode, writing on the terminal directly. When reentering the TUI mode, control is given back to the curses windows. The screen is then refreshed.

This key binding uses the bindable Readline function `tui-switch-mode`.

[C-x 1]

Use a TUI layout with only one window. The layout will either be '`source`'. When the TUI mode is not active, it will switch to the TUI mode.

Think of this key binding as the Emacs [C-x 1] binding.

This key binding uses the bindable Readline function `tui-delete-other-windows`.

[C-x 2]

Use a TUI layout with at least two windows. When the current layout already has two windows, the next layout with two windows is used. When a new layout is chosen, one window will always be common to the previous layout and the new one.

Think of it as the Emacs [C-x 2] binding.

This key binding uses the bindable Readline function `tui-change-windows`.

[C-x o]

Change the active window. The TUI associates several key bindings (like scrolling and arrow keys) with the active window. This command gives the focus to the next TUI window.

Think of it as the Emacs [C-x o] binding.

This key binding uses the bindable Readline function `tui-other-window`.

[C-x s]

Switch in and out of the TUI SingleKey mode that binds single keys to [GDB] commands (see [TUI Single Key Mode](TUI-Single-Key-Mode.html#TUI-Single-Key-Mode)).

This key binding uses the bindable Readline function `next-keymap`.

The following key bindings only work in the TUI mode:

PgUp

Scroll the active window one page up.

PgDn

Scroll the active window one page down.

Up

Scroll the active window one line up.

Down

Scroll the active window one line down.

Left

Scroll the active window one column left.

Right

Scroll the active window one column right.

[C-L]

Refresh the screen.

Because the arrow keys scroll the active window in the TUI mode, they are not available for their normal use by readline unless the command window has the focus. When another window is active, you must use other readline key bindings such as [C-p] to control the command window.

---

::: header
Next: [TUI Single Key Mode](TUI-Single-Key-Mode.html#TUI-Single-Key-Mode)]
:::
