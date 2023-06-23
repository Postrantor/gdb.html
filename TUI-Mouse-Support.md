---
tip: translate by openai@2023-06-23 14:53:26
...
---
description: TUI Mouse Support (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: TUI Mouse Support (Debugging with GDB)
lang: en
resource-type: document
title: TUI Mouse Support (Debugging with GDB)
---------------------------------------------

::: header
Next: [TUI Commands](TUI-Commands.html#TUI-Commands)]
:::

---

### 25.4 TUI Mouse Support

If the curses library supports the mouse, the TUI supports mouse actions.

> 如果 curses 库支持鼠标，TUI 也支持鼠标操作。

The mouse wheel scrolls the appropriate window under the mouse cursor.

> 鼠标滚轮可以滚动鼠标指针下方的适当窗口。

The TUI itself does not directly support copying/pasting with the mouse. However, on Unix terminals, you can typically press and hold the SHIFT key on your keyboard to temporarily bypass [GDB]'s TUI and access the terminal's native mouse copy/paste functionality (commonly, click-drag-release or double-click to select text, middle-click to paste). This copy/paste works with the terminal's selection buffer, as opposed to the TUI's buffer.

> TUI 本身不支持使用鼠标复制/粘贴。但是，在 Unix 终端上，通常可以按住 SHIFT 键以暂时绕过[GDB]的 TUI，并访问终端的本机鼠标复制/粘贴功能（通常，单击拖放或双击选择文本，中键粘贴）。此复制/粘贴使用终端的选择缓冲区，而不是 TUI 的缓冲区。
