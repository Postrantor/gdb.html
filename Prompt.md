---
tip: translate by openai@2023-06-23 12:26:55
...
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

> 在GDB会话中，你可以随时知道你正在与谁交谈。


*Note:* `set prompt` does not add a space for you after the prompt you set. This allows you to set a prompt which ends in a space or a prompt that does not.

> *注意：* `设置提示`不会为您在设置的提示后面添加空格。这使您可以设置以空格结尾或不以空格结尾的提示。

`set prompt newprompt`


Directs [GDB] as its prompt string henceforth.

> 从此以后，将GDB作为其提示字符串进行指引。

`show prompt`


Prints a line of the form: '`Gdb's prompt is: your-prompt`'

> 打印一行格式：'Gdb的提示是：你的提示'


Versions of [GDB] that ship with Python scripting enabled have prompt extensions. The commands for interacting with these extensions are:

> 搭載有Python腳本啟用功能的GDB版本具有提示擴展。與這些擴展交互的命令是：

`set extended-prompt prompt`


Set an extended prompt that allows for substitutions. See [gdb.prompt](gdb_002eprompt.html#gdb_002eprompt), for a list of escape sequences that can be used for substitution. Any escape sequences specified as part of the prompt string are replaced with the corresponding strings each time the prompt is displayed.

> 设置一个允许替换的扩展提示。有关可用于替换的转义序列的列表，请参见[gdb.prompt](gdb_002eprompt.html#gdb_002eprompt)。每次显示提示时，提示字符串中指定的任何转义序列都将替换为相应的字符串。

For example:

::: smallexample

```bash
set extended-prompt Current working directory: \w (gdb)
```

:::

Note that when an extended-prompt is set, it takes control of the `prompt_hook` hook. See [prompt_hook](Basic-Python.html#prompt_005fhook), for further information.

`show extended-prompt`


Prints the extended prompt. Any escape sequences specified as part of the prompt string with `set extended-prompt`, are replaced with the corresponding strings each time the prompt is displayed.

> 打印扩展提示符。每次显示提示符时，使用`set extended-prompt`指定的任何转义序列都会被相应的字符串替换。

---

::: header
Next: [Editing](Editing.html#Editing)]
:::
