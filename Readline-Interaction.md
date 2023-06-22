---
description: Readline Interaction (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Readline Interaction (Debugging with GDB)
lang: en
resource-type: document
title: Readline Interaction (Debugging with GDB)
---
::: header
Next: [Readline Init File](Readline-Init-File.html#Readline-Init-File)]
:::

---

### 33.2 Readline Interaction

Often during an interactive session you type in a long line of text, only to notice that the first word on the line is misspelled. The Readline library gives you a set of commands for manipulating the text as you type it in, allowing you to just fix your typo, and not forcing you to retype the majority of the line. Using these editing commands, you move the cursor to the place that needs correction, and delete or insert the text of the corrections. Then, when you are satisfied with the line, you simply press RET. You do not have to be at the end of the line to press RET; the entire line is accepted regardless of the location of the cursor within the line.

---

• [Readline Bare Essentials](Readline-Bare-Essentials.html#Readline-Bare-Essentials):              The least you need to know about Readline.
• [Readline Movement Commands](Readline-Movement-Commands.html#Readline-Movement-Commands):        Moving about the input line.
• [Readline Killing Commands](Readline-Killing-Commands.html#Readline-Killing-Commands):           How to delete text, and how to get it back!
• [Readline Arguments](Readline-Arguments.html#Readline-Arguments):                                Giving numeric arguments to commands.
• [Searching](Searching.html#Searching):                                                           Searching through previous lines.

---
