---
tip: translate by openai@2023-06-24 00:37:46
...
---
description: Numeric Arguments (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Numeric Arguments (Debugging with GDB)
lang: en
resource-type: document
title: Numeric Arguments (Debugging with GDB)
---
::: header
Next: [Commands For Completion](Commands-For-Completion.html#Commands-For-Completion)]
:::

---

#### 33.4.5 Specifying Numeric Arguments

`digit-argument (M-0, M-1, … M--)`


:   Add this digit to the argument already accumulating, or start a new argument. [M\--] starts a negative argument.

> 加上这个数字到已经累积的参数中，或者开始一个新的参数。[M\--]开始一个负参数。

`universal-argument ()`


:   This is another way to specify an argument. If this command is followed by one or more digits, optionally with a leading minus sign, those digits define the argument. If the command is followed by digits, executing `universal-argument` again ends the numeric argument, but is otherwise ignored. As a special case, if this command is immediately followed by a character that is neither a digit nor minus sign, the argument count for the next command is multiplied by four. The argument count is initially one, so executing this function the first time makes the argument count four, a second time makes the argument count sixteen, and so on. By default, this is not bound to a key.

> 这是另一种指定参数的方式。如果该命令后面跟随一个或多个数字，可选地带有前导负号，这些数字定义了参数。如果命令后面跟随数字，再次执行“universal-argument”会结束数字参数，但其他方面会被忽略。作为一个特殊情况，如果该命令立即跟随一个既不是数字也不是负号的字符，则下一个命令的参数计数将乘以4。参数计数最初为1，因此执行此函数第一次使参数计数为4，第二次使参数计数为16，以此类推。默认情况下，此功能未绑定到任何按键。
