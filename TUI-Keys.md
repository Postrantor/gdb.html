---
tip: translate by openai@2023-06-24 04:15:16
...
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

> TUI安装了几个重要的快捷键到readline键盘映射（参见[命令行编辑](Command-Line-Editing.html#Command-Line-Editing)）。 下面的快捷键在TUI模式和[GDB]标准模式下都可以使用。

[C-x C-a]

[C-x a]

[C-x A]


Enter or leave the TUI mode. When leaving the TUI mode, the curses window management stops and [GDB] operates using its standard mode, writing on the terminal directly. When reentering the TUI mode, control is given back to the curses windows. The screen is then refreshed.

> 进入或退出TUI模式。退出TUI模式时，curses窗口管理停止，[GDB]直接在终端上操作。重新进入TUI模式时，控制权返回到curses窗口。然后刷新屏幕。

This key binding uses the bindable Readline function `tui-switch-mode`.

[C-x 1]


Use a TUI layout with only one window. The layout will either be '`source`'. When the TUI mode is not active, it will switch to the TUI mode.

> 使用只有一个窗口的TUI布局。布局将是“源”。当TUI模式不活跃时，它将切换到TUI模式。

Think of this key binding as the Emacs [C-x 1] binding.


This key binding uses the bindable Readline function `tui-delete-other-windows`.

> 这个键绑定使用可绑定的Readline函数`tui-delete-other-windows`。

[C-x 2]


Use a TUI layout with at least two windows. When the current layout already has two windows, the next layout with two windows is used. When a new layout is chosen, one window will always be common to the previous layout and the new one.

> 使用至少具有两个窗口的图形用户界面布局。当当前布局已经有两个窗口时，将使用下一个具有两个窗口的布局。当选择新的布局时，一个窗口将始终与前一个布局和新布局相同。

Think of it as the Emacs [C-x 2] binding.


This key binding uses the bindable Readline function `tui-change-windows`.

> 这个键绑定使用可绑定的Readline函数`tui-change-windows`。

[C-x o]


Change the active window. The TUI associates several key bindings (like scrolling and arrow keys) with the active window. This command gives the focus to the next TUI window.

> 更改活动窗口。TUI将几个键绑定（如滚动和箭头键）与活动窗口相关联。此命令将焦点移到下一个TUI窗口。

Think of it as the Emacs [C-x o] binding.

This key binding uses the bindable Readline function `tui-other-window`.

[C-x s]


Switch in and out of the TUI SingleKey mode that binds single keys to [GDB] commands (see [TUI Single Key Mode](TUI-Single-Key-Mode.html#TUI-Single-Key-Mode)).

> 切换到和退出TUI单键模式，该模式将单个键绑定到[GDB]命令（参见[TUI单键模式]（TUI-Single-Key-Mode.html#TUI-Single-Key-Mode））。

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

> 由于箭头键在TUI模式下可以滚动活动窗口，因此除非命令窗口获得焦点，否则它们无法正常使用readline。当另一个窗口处于活动状态时，您必须使用其他readline键绑定，例如[C-p]来控制命令窗口。

---

::: header
Next: [TUI Single Key Mode](TUI-Single-Key-Mode.html#TUI-Single-Key-Mode)]
:::
