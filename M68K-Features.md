---
tip: translate by openai@2023-06-24 10:29:15
...
---
description: M68K Features (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: M68K Features (Debugging with GDB)
lang: en
resource-type: document
title: M68K Features (Debugging with GDB)
---
::: header
Next: [NDS32 Features](NDS32-Features.html#NDS32-Features)]
:::

---

#### G.5.8 M68K Features

`‘org.gnu.gdb.m68k.core’`
`‘org.gnu.gdb.coldfire.core’`
`‘org.gnu.gdb.fido.core’`


:   One of those features must be always present. The feature that is present determines which flavor of m68k is used. The feature that is present should contain registers '`d0`'.

> 一个这些特性必须总是存在的。存在的特性决定使用哪种m68k风味。存在的特性应包含寄存器'd0'。

`‘org.gnu.gdb.coldfire.fp’`


:   This feature is optional. If present, it should contain registers '`fp0`'.

> 这个功能是可选的。如果存在，它应该包含寄存器'fp0'。

```
Note that, despite the fact that this feature's name says '`coldfire`', then 64-bit floating point registers are required.
```
