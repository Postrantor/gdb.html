---
description: History Interaction (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: History Interaction (Debugging with GDB)
lang: en
resource-type: document
title: History Interaction (Debugging with GDB)
---
::: header
Up: [Using History Interactively](Using-History-Interactively.html#Using-History-Interactively)]
:::

---

### 34.1 History Expansion

The History library provides a history expansion feature that is similar to the history expansion provided by `csh`. This section describes the syntax used to manipulate the history information.

History expansions introduce words from the history list into the input stream, making it easy to repeat commands, insert the arguments to a previous command into the current input line, or fix errors in previous commands quickly.

History expansion takes place in two parts. The first is to determine which line from the history list should be used during substitution. The second is to select portions of that line for inclusion into the current one. The line selected from the history is called the *event*, and the portions of that line that are acted upon are called *words*. Various *modifiers* are available to manipulate the selected words. The line is broken into words in the same fashion that Bash does, so that several words surrounded by quotes are considered one word. History expansions are introduced by the appearance of the history expansion character, which is '`!`' by default.

History expansion implements shell-like quoting conventions: a backslash can be used to remove the special handling for the next character; single quotes enclose verbatim sequences of characters, and can be used to inhibit history expansion; and characters enclosed within double quotes may be subject to history expansion, since backslash can escape the history expansion character, but single quotes may not, since they are not treated specially within double quotes.

---

• [Event Designators](Event-Designators.html#Event-Designators):        How to specify which history line to use.
• [Word Designators](Word-Designators.html#Word-Designators):           Specifying which words are of interest.
• [Modifiers](Modifiers.html#Modifiers):                                Modifying the results of substitution.

---

---

::: header
Up: [Using History Interactively](Using-History-Interactively.html#Using-History-Interactively)]
:::
