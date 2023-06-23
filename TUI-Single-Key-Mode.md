---
tip: translate by openai@2023-06-23 14:55:49
...
---
description: TUI Single Key Mode (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: TUI Single Key Mode (Debugging with GDB)
lang: en
resource-type: document
title: TUI Single Key Mode (Debugging with GDB)
-----------------------------------------------

::: header
Next: [TUI Mouse Support](TUI-Mouse-Support.html#TUI-Mouse-Support)]
:::

---

### 25.3 TUI Single Key Mode

The TUI also provides a *SingleKey* mode, which binds several frequently used [GDB] to switch into this mode, where the following key bindings are used:

> TUI 也提供了 *SingleKey* 模式，它将一些常用的[GDB]绑定到此模式，其中使用以下键绑定：

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

> 下一步。快捷键字母 `o` 代表"跳过"。

[q]

exit the SingleKey mode.

> 退出单键模式。

[r]

run

[s]

step

[i]

stepi. The shortcut letter '`i`' stands for "step Into".

> 步入（Stepi）。快捷字母“i”代表“步入（Step Into）”。

[u]

up

[v]

info locals

[w]

where

Other keys temporarily switch to the [GDB].

> 其他键暂时切换到[GDB]。

If [GDB] to add additional bindings to this keymap.

> 如果要为该键映射添加额外的绑定，请使用 GDB。
