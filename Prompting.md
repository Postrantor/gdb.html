---
tip: translate by openai@2023-06-24 01:34:08
...
---
description: Prompting (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Prompting (Debugging with GDB)
lang: en
resource-type: document
title: Prompting (Debugging with GDB)
---
::: header
Next: [Errors](Errors.html#Errors)]
:::

---

### 28.3 Annotation for [GDB]


When [GDB] prompts for input, it annotates this fact so it is possible to know when to send output, when the output from a given command is over, etc.

> 当GDB提示输入时，它会标注这一事实，因此可以知道何时发送输出，给定命令的输出结束时等等。


Different kinds of input each have a different *input type*. Each input type has three annotations: a `pre-` annotation, which denotes the beginning of any prompt which is being output, a plain annotation, which denotes the end of the prompt, and then a `post-` annotation which denotes the end of any echo which may (or may not) be associated with the input. For example, the `prompt` input type features the following annotations:

> 不同类型的输入都有不同的输入类型。每种输入类型都有三个注释：`pre-`注释，表示任何输出提示的开始；普通注释，表示提示的结束；以及`post-`注释，表示任何可能（或不可能）与输入相关的回声的结束。例如，`prompt`输入类型具有以下注释：

::: smallexample

```bash
^Z^Zpre-prompt
^Z^Zprompt
^Z^Zpost-prompt
```

:::

The input types are

`prompt`

When [GDB] prompt).

`commands`


When [GDB] prompts for a set of commands, like in the `commands` command. The annotations are repeated for each command which is input.

> 当GDB提示输入一组命令，就像在`commands`命令中一样，每个输入的命令都会重复注释。

`overload-choice`

When [GDB] wants the user to select between various overloaded functions.

`query`

When [GDB] wants the user to confirm a potentially dangerous operation.

`prompt-for-continue`


When [GDB] is asking the user to press return to continue. Note: Don't expect this to work well; instead use `set height 0` to disable prompting. This is because the counting of lines is buggy in the presence of annotations.

> 当[GDB]要求用户按下回车继续时，不要指望这能奏效；相反，请使用`set height 0`来禁用提示。这是因为在存在注释时，行数计算存在错误。

---

::: header
Next: [Errors](Errors.html#Errors)]
:::
