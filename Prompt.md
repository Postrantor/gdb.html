---
description: Prompt (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Prompt (Debugging with GDB)
lang: en
resource-type: document
title: Prompt (Debugging with GDB)
---
::: header
Next: [Editing](Editing.html#Editing)]
:::

---

### 22.1 Prompt

[GDB] sessions so that you can always tell which one you are talking to.

*Note:* `set prompt` does not add a space for you after the prompt you set. This allows you to set a prompt which ends in a space or a prompt that does not.

`set prompt newprompt`

Directs [GDB] as its prompt string henceforth.

`show prompt`

Prints a line of the form: '`Gdb's prompt is: your-prompt`'

Versions of [GDB] that ship with Python scripting enabled have prompt extensions. The commands for interacting with these extensions are:

`set extended-prompt prompt`

Set an extended prompt that allows for substitutions. See [gdb.prompt](gdb_002eprompt.html#gdb_002eprompt), for a list of escape sequences that can be used for substitution. Any escape sequences specified as part of the prompt string are replaced with the corresponding strings each time the prompt is displayed.

For example:

::: smallexample

```bash
set extended-prompt Current working directory: \w (gdb)
```

:::

Note that when an extended-prompt is set, it takes control of the `prompt_hook` hook. See [prompt_hook](Basic-Python.html#prompt_005fhook), for further information.

`show extended-prompt`

Prints the extended prompt. Any escape sequences specified as part of the prompt string with `set extended-prompt`, are replaced with the corresponding strings each time the prompt is displayed.

---

::: header
Next: [Editing](Editing.html#Editing)]
:::
