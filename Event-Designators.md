---
description: Event Designators (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Event Designators (Debugging with GDB)
lang: en
resource-type: document
title: Event Designators (Debugging with GDB)
---
::: header
Next: [Word Designators](Word-Designators.html#Word-Designators)]
:::

---

#### 34.1.1 Event Designators

An event designator is a reference to a command line entry in the history list. Unless the reference is absolute, events are relative to the current position in the history list.

`!`

:   Start a history substitution, except when followed by a space, tab, the end of the line, or '`=`'.

`!n`

:   Refer to command line `n`.

`!-n`

:   Refer to the command `n` lines back.

`!!`

:   Refer to the previous command. This is a synonym for '`!-1`'.

`!string`

:   Refer to the most recent command preceding the current position in the history list starting with `string`.

`!?string[?]`

:   Refer to the most recent command preceding the current position in the history list containing `string` is missing, the string from the most recent search is used; it is an error if there is no previous search string.

`^string1^string2^`

:   Quick Substitution. Repeat the last command, replacing `string1`. Equivalent to `!!:s^string1^string2^`.

`!#`

:   The entire command line typed so far.
