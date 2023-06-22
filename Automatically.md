---
description: Automatically (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Automatically (Debugging with GDB)
lang: en
resource-type: document
title: Automatically (Debugging with GDB)
---
::: header
Previous: [Manually](Manually.html#Manually)]
:::

---

#### 15.1.3 Having [GDB]

To have [GDB] issues a warning.

This may not seem necessary for most programs, which are written entirely in one source language. However, program modules and libraries written in one source language can be used by a main program written in a different source language. Using '`set language auto`' in this case frees you from having to set the working language manually.
