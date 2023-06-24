---
tip: translate by openai@2023-06-23 23:46:00
...
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

> 停止保存输入到当前键盘宏的字符，并保存定义。

`call-last-kbd-macro (C-x e)`


:   Re-execute the last keyboard macro defined, by making the characters in the macro appear as if typed at the keyboard.

> 重新执行上一个定义的键盘宏，使得宏中的字符就像在键盘上输入一样出现。

`print-last-kbd-macro ()`


:   Print the last keboard macro defined in a format suitable for the `inputrc` file.

> 打印最后一个键盘宏，以`inputrc`文件中的格式输出。
