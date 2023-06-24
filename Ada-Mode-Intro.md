---
tip: translate by openai@2023-06-23 16:58:51
...
---
description: Ada Mode Intro (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Ada Mode Intro (Debugging with GDB)
lang: en
resource-type: document
title: Ada Mode Intro (Debugging with GDB)
---
::: header
Next: [Omissions from Ada](Omissions-from-Ada.html#Omissions-from-Ada)]
:::

---

#### 15.4.10.1 Introduction


The Ada mode of [GDB] supports a fairly large subset of Ada expression syntax, with some extensions. The philosophy behind the design of this subset is

> GDB的Ada模式支持相当大的Ada表达式语法子集，具有一些扩展。这个子集设计背后的哲学是

- That [GDB]).

- That type safety and strict adherence to Ada language restrictions are not particularly important to the [GDB] user.

> 那种类型安全性和严格遵守Ada语言限制对GDB用户并不是特别重要。
- That brevity is important to the [GDB] user.


Thus, for brevity, the debugger acts as if all names declared in user-written packages are directly visible, even if they are not visible according to Ada rules, thus making it unnecessary to fully qualify most names with their packages, regardless of context. Where this causes ambiguity, [GDB] asks the user's intent.

> 因此，为了简洁，调试器按照用户编写的包中声明的所有名称直接可见的方式行事，即使根据Ada规则它们不可见，因此无需完全根据上下文使用大量的包来限定名称。当引起歧义时，[GDB]会询问用户的意图。


The debugger will start in Ada mode if it detects an Ada main program. As for other languages, it will enter Ada mode when stopped in a program that was translated from an Ada source file.

> 调试器如果检测到一个Ada主程序，就会以Ada模式启动。至于其他语言，当在翻译自Ada源文件的程序中停止时，它就会进入Ada模式。


While in Ada mode, you may use '\--' for comments. This is useful mostly for documenting command files. The standard [GDB]') still works at the beginning of a line in Ada mode, but not in the middle (to allow based literals).

> 在Ada模式下，可以使用'\--'作为注释。这对文档化命令文件特别有用。标准[GDB]在Ada模式下仍然可以在行首使用，但不能在中间使用（以允许基于文字的文字）。
