---
tip: translate by openai@2023-06-23 14:50:18
...
---
description: TUI Commands (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: TUI Commands (Debugging with GDB)
lang: en
resource-type: document
title: TUI Commands (Debugging with GDB)
---
::: header
Next: [TUI Configuration](TUI-Configuration.html#TUI-Configuration)]
:::

---

### 25.5 TUI-specific Commands


The TUI has specific commands to control the text windows. These commands are always available, even when [GDB] is in the standard mode, most of these commands will automatically switch to the TUI mode.

> TUI有特定的命令来控制文本窗口。即使[GDB]处于标准模式时，这些命令也始终可用，大多数这些命令会自动切换到TUI模式。

Note that if [GDB] Interface](GDB_002fMI.html#GDB_002fMI)), most of these commands will fail with an error, because it would not be possible or desirable to enable curses window management.

`tui enable`

:

```
Activate TUI mode. The last active TUI window layout will be used if TUI mode has previously been used in the current debugging session, otherwise a default layout is used.
```

`tui disable`

:

```
Disable TUI mode, returning to the console interpreter.


```

`info win`

:

```
List the names and sizes of all currently displayed windows.
```

`tui new-layout name window weight [window weight…]`

:

```
Create a new TUI layout. The new layout will be named `name`, and can be accessed using the `layout` command (see below).

Each `window` parameter is either the name of a window to display, or a window description. The windows will be displayed from top to bottom in the order listed.

The names of the windows are the same as the ones given to the `focus` command (see below); additional, the `status` window can be specified. Note that, because it is of fixed height, the weight assigned to the status window is of no importance. It is conventional to use '`0`' here.

A window description looks a bit like an invocation of `tui new-layout`, and is of the form .

This specifies a sub-layout. If `-horizontal` is given, the windows in this description will be arranged side-by-side, rather than top-to-bottom.

Each `weight` is an integer. It is the weight of this window relative to all the other windows in the layout. These numbers are used to calculate how much of the screen is given to each window.

For example:

::: example
``` example

(gdb) tui new-layout example src 1 regs 1 status 0 cmd 1

> (gdb) tui新布局示例源代码1寄存器1状态0命令1
```

:::

Here, the new layout is called '`example`'. It shows the source and register windows, followed by the status window, and then finally the command window. The non-status windows all have the same weight, so the terminal will be split into three roughly equal sections.

Here is a more complex example, showing a horizontal layout:

::: example

```example

(gdb) tui new-layout example  2 status 0 cmd 1

> (gdb) tui 新布局示例  2 状态 0 命令 1
```

:::

This will result in side-by-side source and assembly windows; with the status and command window being beneath these, filling the entire width of the terminal. Because they have weight 2, the source and assembly windows will be twice the height of the command window.

```

`tui layout name`
`layout name`


:   Changes which TUI windows are displayed. The `name` parameter controls which layout is shown. It can be either one of the built-in layout names, or the name of a layout defined by the user using `tui new-layout`.

> 更改显示的TUI窗口。`name`参数控制显示哪种布局。它可以是内置布局名称之一，也可以是使用`tui new-layout`定义的布局的名称。

```

The built-in layouts are as follows:

`next`

:   Display the next layout.

`prev`

:   Display the previous layout.

`src`

:   Display the source and command windows.

`asm`

:   Display the assembly and command windows.

`split`

:   Display the source, assembly, and command windows.

`regs`

:   When in `src` layout display the register, source, and command windows. When in `asm` or `split` layout display the register, assembler, and command windows.

```

`tui focus name`
`focus name`


:   Changes which TUI window is currently active for scrolling. The `name` parameter can be any of the following:

> 更改当前活动的TUI窗口以进行滚动。`name`参数可以是以下任何一项：

```

`next`

:   Make the next window active for scrolling.

`prev`

:   Make the previous window active for scrolling.

`src`

:   Make the source window active for scrolling.

`asm`

:   Make the assembly window active for scrolling.

`regs`

:   Make the register window active for scrolling.

`cmd`

:   Make the command window active for scrolling.

```

`tui refresh`
`refresh`


:   Refresh the screen. This is similar to typing [C-L].

> 刷新屏幕。这与敲击[C-L]类似。

`tui reg group`

:   

```

Changes the register group displayed in the tui register window to `group`. If the register window is not currently displayed this command will cause the register window to be displayed. The list of register groups, as well as their order is target specific. The following groups are available on most targets:

`next`

:   Repeatedly selecting this group will cause the display to cycle through all of the available register groups.

`prev`

:   Repeatedly selecting this group will cause the display to cycle through all of the available register groups in the reverse order to `next`.

`general`

:   Display the general registers.

`float`

:   Display the floating point registers.

`system`

:   Display the system registers.

`vector`

:   Display the vector registers.

`all`

:   Display all registers.

```

`update`

:   

```

Update the source window and the current execution point.

```

`tui window height name +count`
`tui window height name -count`
`winheight name +count`
`winheight name -count`


:   Change the height of the window `name` (see [info win](#info_005fwin_005fcommand)).

> 改变窗口`name`的高度（参见[info win](#info_005fwin_005fcommand)）。

```

The set of currently visible windows must always fill the terminal, and so, it is only possible to resize on window if there are other visible windows that can either give or receive the extra terminal space.

```

`tui window width name +count`
`tui window width name -count`
`winwidth name +count`
`winwidth name -count`


:   Change the width of the window `name` parameter can be the name of any currently visible window. The names of the currently visible windows can be discovered using `info win` (see [info win](#info_005fwin_005fcommand)).

> 更改窗口`name`参数的宽度，`name`参数可以是当前可见窗口的任何名称。当前可见窗口的名称可以使用`info win`发现（参见[info win](#info_005fwin_005fcommand))。

```

The set of currently visible windows must always fill the terminal, and so, it is only possible to resize on window if there are other visible windows that can either give or receive the extra terminal space.

```

---

::: header
Next: [TUI Configuration](TUI-Configuration.html#TUI-Configuration)]
:::
```
