---
description: Keyboard Macros (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Keyboard Macros (Debugging with GDB)
lang: en
resource-type: document
title: Keyboard Macros (Debugging with GDB)
---
::: header
Next: [Miscellaneous Commands](Miscellaneous-Commands.html#Miscellaneous-Commands)]
:::

---

#### 33.4.7 Keyboard Macros

`start-kbd-macro (C-x ()`

:   Begin saving the characters typed into the current keyboard macro.

`end-kbd-macro (C-x ))`

:   Stop saving the characters typed into the current keyboard macro and save the definition.

`call-last-kbd-macro (C-x e)`

:   Re-execute the last keyboard macro defined, by making the characters in the macro appear as if typed at the keyboard.

`print-last-kbd-macro ()`

:   Print the last keboard macro defined in a format suitable for the `inputrc` file.