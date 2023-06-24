---
tip: translate by openai@2023-06-24 00:30:16
...
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

> 在可选的词语指示符之后，您可以添加一个或多个以“：”开头的修饰符序列。这些修饰符会修改或编辑从历史事件中选择的单词或单词。

`h`

:   Remove a trailing pathname component, leaving only the head.

`t`

:   Remove all leading pathname components, leaving the tail.

`r`


:   Remove a trailing suffix of the form '`.suffix`', leaving the basename.

> 移除以'`.suffix`'形式结尾的后缀，保留基本名称。

`e`

:   Remove all but the trailing suffix.

`p`

:   Print the new command but do not execute it.

`s/old/new/`


:   Substitute `new` is deleted. The final delimiter is optional if it is the last character on the input line.

> 替换`新的`被删除了。如果最后一个字符是分隔符，则可以省略最后的分隔符。

`&`

:   Repeat the previous substitution.

`g`
`a`


:   Cause changes to be applied over the entire event line. Used in conjunction with '`s`'.

> 使更改应用于整个事件线。与“s”结合使用。

`G`

:   Apply the following '`s`' modifier once to each word in the event.
