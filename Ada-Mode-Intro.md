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

- That [GDB]).
- That type safety and strict adherence to Ada language restrictions are not particularly important to the [GDB] user.
- That brevity is important to the [GDB] user.

Thus, for brevity, the debugger acts as if all names declared in user-written packages are directly visible, even if they are not visible according to Ada rules, thus making it unnecessary to fully qualify most names with their packages, regardless of context. Where this causes ambiguity, [GDB] asks the user's intent.

The debugger will start in Ada mode if it detects an Ada main program. As for other languages, it will enter Ada mode when stopped in a program that was translated from an Ada source file.

While in Ada mode, you may use '\--' for comments. This is useful mostly for documenting command files. The standard [GDB]') still works at the beginning of a line in Ada mode, but not in the middle (to allow based literals).
