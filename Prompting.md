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

Different kinds of input each have a different *input type*. Each input type has three annotations: a `pre-` annotation, which denotes the beginning of any prompt which is being output, a plain annotation, which denotes the end of the prompt, and then a `post-` annotation which denotes the end of any echo which may (or may not) be associated with the input. For example, the `prompt` input type features the following annotations:

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

`overload-choice`

When [GDB] wants the user to select between various overloaded functions.

`query`

When [GDB] wants the user to confirm a potentially dangerous operation.

`prompt-for-continue`

When [GDB] is asking the user to press return to continue. Note: Don't expect this to work well; instead use `set height 0` to disable prompting. This is because the counting of lines is buggy in the presence of annotations.

---

::: header
Next: [Errors](Errors.html#Errors)]
:::
