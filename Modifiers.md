---
description: Modifiers (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Modifiers (Debugging with GDB)
lang: en
resource-type: document
title: Modifiers (Debugging with GDB)
---
::: header
Previous: [Word Designators](Word-Designators.html#Word-Designators)]
:::

---

#### 34.1.3 Modifiers

After the optional word designator, you can add a sequence of one or more of the following modifiers, each preceded by a '`:`'. These modify, or edit, the word or words selected from the history event.

`h`

:   Remove a trailing pathname component, leaving only the head.

`t`

:   Remove all leading pathname components, leaving the tail.

`r`

:   Remove a trailing suffix of the form '`.suffix`', leaving the basename.

`e`

:   Remove all but the trailing suffix.

`p`

:   Print the new command but do not execute it.

`s/old/new/`

:   Substitute `new` is deleted. The final delimiter is optional if it is the last character on the input line.

`&`

:   Repeat the previous substitution.

`g`
`a`

:   Cause changes to be applied over the entire event line. Used in conjunction with '`s`'.

`G`

:   Apply the following '`s`' modifier once to each word in the event.
