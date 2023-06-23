---
description: Setting (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Setting (Debugging with GDB)
lang: en
resource-type: document
title: Setting (Debugging with GDB)
---
::: header
Next: [Show](Show.html#Show)]
:::

---

### 15.1 Switching Between Source Languages

There are two ways to control the working language---either have [GDB] defaults to setting the language automatically. The working language is used to determine how expressions you type are interpreted, how values are printed, etc.

In addition to the working language, every source file that [GDB], but you can set the language associated with a filename extension. See [Displaying the Language](Show.html#Show).

This is most commonly a problem when you use a program, such as `cfront` or `f2c`, that generates C but is written in another language. In that case, make the program use `#line` directives in its C output; that way [GDB] will know the correct language of the source code of the original program, and will display that source code, not the generated C code.

---

• [Filenames](Filenames.html#Filenames):                    Filename extensions and languages.
• [Manually](Manually.html#Manually):                       Setting the working language manually
• [Automatically](Automatically.html#Automatically) infer the source language

---

---

::: header
Next: [Show](Show.html#Show)]
:::
