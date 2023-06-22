---
description: Word Designators (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Word Designators (Debugging with GDB)
lang: en
resource-type: document
title: Word Designators (Debugging with GDB)
---
::: header
Next: [Modifiers](Modifiers.html#Modifiers)]
:::

---

#### 34.1.2 Word Designators

Word designators are used to select desired words from the event. A '`:`'. Words are numbered from the beginning of the line, with the first word being denoted by 0 (zero). Words are inserted into the current line separated by single spaces.

For example,

`!!`

:   designates the preceding command. When you type this, the preceding command is repeated in toto.

`!!:$`

:   designates the last argument of the preceding command. This may be shortened to `!$`.

`!fi:2`

:   designates the second argument of the most recent command starting with the letters `fi`.

Here are the word designators:

`0 (zero)`

:   The `0` th word. For many applications, this is the command word.

`n`

:   The `n` th word.

`^`

:   The first argument; that is, word 1.

`$`

:   The last argument.

`%`

:   The first word matched by the most recent '`?string?`' search, if the search string begins with a character that is part of a word.

`x-y`

:   A range of words; '`-y`'.

`*`

:   All of the words, except the `0` th. This is a synonym for '`1-$`' if there is just one word in the event; the empty string is returned in that case.

`x*`

:   Abbreviates '`x-$`'

`x-`

:   Abbreviates '`x-$`' is missing, it defaults to 0.

If a word designator is supplied without an event specification, the previous command is used as the event.

---

::: header
Next: [Modifiers](Modifiers.html#Modifiers)]
:::
