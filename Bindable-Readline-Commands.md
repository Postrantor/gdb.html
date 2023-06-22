---
description: Bindable Readline Commands (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Bindable Readline Commands (Debugging with GDB)
lang: en
resource-type: document
title: Bindable Readline Commands (Debugging with GDB)
---
::: header
Next: [Readline vi Mode](Readline-vi-Mode.html#Readline-vi-Mode)]
:::

---

### 33.4 Bindable Readline Commands

---

• [Commands For Moving](Commands-For-Moving.html#Commands-For-Moving):                    Moving about the line.
• [Commands For History](Commands-For-History.html#Commands-For-History):                 Getting at previous lines.
• [Commands For Text](Commands-For-Text.html#Commands-For-Text):                          Commands for changing text.
• [Commands For Killing](Commands-For-Killing.html#Commands-For-Killing):                 Commands for killing and yanking.
• [Numeric Arguments](Numeric-Arguments.html#Numeric-Arguments):                          Specifying numeric arguments, repeat counts.
• [Commands For Completion](Commands-For-Completion.html#Commands-For-Completion):        Getting Readline to do the typing for you.
• [Keyboard Macros](Keyboard-Macros.html#Keyboard-Macros):                                Saving and re-executing typed characters
• [Miscellaneous Commands](Miscellaneous-Commands.html#Miscellaneous-Commands):           Other miscellaneous commands.

---

This section describes Readline commands that may be bound to key sequences. Command names without an accompanying key sequence are unbound by default.

In the following descriptions, *point* refers to the current cursor position, and *mark* refers to a cursor position saved by the `set-mark` command. The text between the point and mark is referred to as the *region*.
