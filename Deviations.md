---
description: Deviations (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Deviations (Debugging with GDB)
lang: en
resource-type: document
title: Deviations (Debugging with GDB)
---
::: header
Next: [M2 Checks](M2-Checks.html#M2-Checks)]
:::

---

#### 15.4.9.6 Deviations from Standard Modula-2

A few changes have been made to make Modula-2 programs easier to debug. This is done primarily via loosening its type strictness:

- Unlike in standard Modula-2, pointer constants can be formed by integers. This allows you to modify pointer variables during debugging. (In standard Modula-2, the actual address contained in a pointer variable is hidden from you; it can only be modified through direct assignment to another pointer variable or expression that returned a pointer.)
- C escape sequences can be used in strings and characters to represent non-printable characters. [GDB]' format.
- The assignment operator (`:=`) returns the value of its right-hand argument.
- All built-in procedures both modify *and* return their argument.
