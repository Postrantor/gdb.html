---
description: TUI Mouse Support (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: TUI Mouse Support (Debugging with GDB)
lang: en
resource-type: document
title: TUI Mouse Support (Debugging with GDB)
---
::: header
Next: [TUI Commands](TUI-Commands.html#TUI-Commands)]
:::

---

### 25.4 TUI Mouse Support

If the curses library supports the mouse, the TUI supports mouse actions.

The mouse wheel scrolls the appropriate window under the mouse cursor.

The TUI itself does not directly support copying/pasting with the mouse. However, on Unix terminals, you can typically press and hold the SHIFT key on your keyboard to temporarily bypass [GDB]'s TUI and access the terminal's native mouse copy/paste functionality (commonly, click-drag-release or double-click to select text, middle-click to paste). This copy/paste works with the terminal's selection buffer, as opposed to the TUI's buffer.
