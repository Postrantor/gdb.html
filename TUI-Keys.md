---
tip: translate by openai@2023-06-23 14:51:29
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

> TUI安装了几个关键绑定在readline keymaps（参见[命令行编辑](Command-Line-Editing.html#Command-Line-Editing)）。以下关键绑定为TUI模式和[GDB]标准模式安装。

[C-x C-a]

[C-x a]

[C-x A]


Enter or leave the TUI mode. When leaving the TUI mode, the curses window management stops and [GDB] operates using its standard mode, writing on the terminal directly. When reentering the TUI mode, control is given back to the curses windows. The screen is then refreshed.

> 进入或离开TUI模式。当离开TUI模式时，curses窗口管理停止，[GDB]直接使用其标准模式在终端上进行操作。重新进入TUI模式时，控制权将返回到curses窗口。然后刷新屏幕。


This key binding uses the bindable Readline function `tui-switch-mode`.

> 这个键绑定使用可绑定的Readline函数“tui-switch-mode”。

[C-x 1]


Use a TUI layout with only one window. The layout will either be '`source`'. When the TUI mode is not active, it will switch to the TUI mode.

> 使用只有一个窗口的TUI布局。布局将是'源'。当TUI模式不活动时，它将切换到TUI模式。


Think of this key binding as the Emacs [C-x 1] binding.

> 把这个键绑定想象成Emacs的[C-x 1]绑定。


This key binding uses the bindable Readline function `tui-delete-other-windows`.

> 这个键绑定使用可绑定的Readline函数`tui-delete-other-windows`。

[C-x 2]


Use a TUI layout with at least two windows. When the current layout already has two windows, the next layout with two windows is used. When a new layout is chosen, one window will always be common to the previous layout and the new one.

> 使用至少有两个窗口的TUI布局。当当前布局已经有两个窗口时，将使用具有两个窗口的下一个布局。当选择新的布局时，一个窗口将始终与先前的布局和新布局保持一致。


Think of it as the Emacs [C-x 2] binding.

> 想想它就像是 Emacs 的 [C-x 2] 绑定。


This key binding uses the bindable Readline function `tui-change-windows`.

> 这个键绑定使用可绑定的Readline函数`tui-change-windows`。

[C-x o]


Change the active window. The TUI associates several key bindings (like scrolling and arrow keys) with the active window. This command gives the focus to the next TUI window.

> 更改活动窗口。TUI将多个键绑定（如滚动和箭头键）与活动窗口相关联。此命令将焦点移到下一个TUI窗口。


Think of it as the Emacs [C-x o] binding.

> 想想它就像是 Emacs 的 [C-x o] 绑定。


This key binding uses the bindable Readline function `tui-other-window`.

> 这个键绑定使用可绑定的Readline函数“tui-other-window”。

[C-x s]


Switch in and out of the TUI SingleKey mode that binds single keys to [GDB] commands (see [TUI Single Key Mode](TUI-Single-Key-Mode.html#TUI-Single-Key-Mode)).

> 切换进入和退出TUI单键模式，该模式将单个键绑定到[GDB]命令（请参见[TUI单键模式]（TUI-Single-Key-Mode.html#TUI-Single-Key-Mode））。


This key binding uses the bindable Readline function `next-keymap`.

> 这个键绑定使用可绑定的Readline函数`next-keymap`。


The following key bindings only work in the TUI mode:

> 以下快捷键仅在TUI模式下有效：

PgUp


Scroll the active window one page up.

> 滚动活动窗口向上翻一页。

PgDn


Scroll the active window one page down.

> 向下滚动当前窗口一页。

Up


Scroll the active window one line up.

> 向上滚动活动窗口一行。

Down


Scroll the active window one line down.

> 向下滚动活动窗口一行。

Left


Scroll the active window one column left.

> 向左滚动活动窗口一列。

Right


Scroll the active window one column right.

> 滚动活动窗口右移一列。

[C-L]

Refresh the screen.


Because the arrow keys scroll the active window in the TUI mode, they are not available for their normal use by readline unless the command window has the focus. When another window is active, you must use other readline key bindings such as [C-p] to control the command window.

> 由于箭头键在TUI模式下可以滚动活动窗口，因此除非命令窗口获得焦点，否则它们不能用于readline的正常使用。当另一个窗口处于活动状态时，您必须使用其他readline键绑定，例如[C-p]来控制命令窗口。

---

::: header
Next: [TUI Single Key Mode](TUI-Single-Key-Mode.html#TUI-Single-Key-Mode)]
:::
