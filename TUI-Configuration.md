---
tip: translate by openai@2023-06-24 04:14:59
...
---
description: TUI Configuration (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: TUI Configuration (Debugging with GDB)
lang: en
resource-type: document
title: TUI Configuration (Debugging with GDB)
---
::: header
Previous: [TUI Commands](TUI-Commands.html#TUI-Commands)]
:::

---

### 25.6 TUI Configuration Variables

Several configuration variables control the appearance of TUI windows.

`set tui border-kind kind`

:

```
Select the border appearance for the source, assembly and register windows. The possible values are the following:

`space`

:   Use a space character to draw the border.

`ascii`

:   Use [ASCII]' to draw the border.

`acs`

:   Use the Alternate Character Set to draw the border. The border is drawn using character line graphics if the terminal supports them.
```

| `set tui border-mode mode` |
| :------------------------: |

`set tui active-border-mode mode`

:

```
Select the display attributes for the borders of the inactive windows or the active window. The `mode` can be one of the following:

`normal`

:   Use normal attributes to display the border.

`standout`

:   Use standout mode.

`reverse`

:   Use reverse video mode.

`half`

:   Use half bright mode.

`half-standout`

:   Use half bright and standout mode.

`bold`

:   Use extra bright or bold mode.

`bold-standout`

:   Use extra bright or bold and standout mode.
```

`set tui tab-width nchars`

:

```
Set the width of tab stops to be `nchars` characters. This setting affects the display of TAB characters in the source and assembly windows.
```

`set tui compact-source [on|off]`

:

```
Set whether the TUI source window is displayed in "compact" form. The default display uses more space for line numbers; the compact display uses only as much space as is needed for the line numbers in the current file.


```

`set debug tui [on|off]`


:   Turn on or off display of [GDB] internal debug messages relating to the TUI.

> 开启或关闭[GDB] TUI的内部调试消息的显示。

```

```

`show debug tui`


:   Show the current status of displaying [GDB] internal debug messages relating to the TUI.

> 显示有关TUI的GDB内部调试消息的当前状态。


Note that the colors of the TUI borders can be controlled using the appropriate `set style` commands. See [Output Styling](Output-Styling.html#Output-Styling).

> 注意，可以使用适当的`set style`命令来控制TUI边框的颜色。请参见[输出样式](Output-Styling.html#Output-Styling)。

---

::: header
Previous: [TUI Commands](TUI-Commands.html#TUI-Commands)]
:::
