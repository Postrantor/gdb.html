---
tip: translate by openai@2023-06-23 20:45:36
...
---
description: Edit (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Edit (Debugging with GDB)
lang: en
resource-type: document
title: Edit (Debugging with GDB)
---
::: header
Next: [Search](Search.html#Search)]
:::

---

### 9.3 Editing Source Files


To edit the lines in a source file, use the `edit` command. The editing program of your choice is invoked with the current line set to the active line in the program. Alternatively, there are several ways to specify what part of the file you want to print if you want to see other parts of the program:

> 使用`edit`命令编辑源文件中的行。您选择的编辑程序将以程序中的当前行为活动行调用。另外，如果要查看程序的其他部分，还有几种方法可以指定要打印的文件部分：

`edit locspec`


:   Edit the source file of the code location that results from resolving `locspec`. Editing starts at the source file and source line `locspec` resolves to. See [Location Specifications](Location-Specifications.html#Location-Specifications), for all the possible forms of the `locspec` argument.

> 编辑由`locspec`解析而来的代码位置的源文件。编辑从`locspec`解析到的源文件和源行开始。有关所有可能的`locspec`参数形式，请参阅[位置规范](Location-Specifications.html#Location-Specifications)。

```
If `locspec` resolves to more than one source line in your program, then the command prints the list of resolved source lines and does not proceed with the editing.

Here are the forms of the `edit` command most commonly used:

`edit number`

:   Edit the current source file with `number` as the active line number.

`edit function`

:   Edit the file containing `function` at the beginning of its definition.
```

#### 9.3.1 Choosing your Editor


You can customize [GDB] to use the `vi` editor, you could use these commands with the `sh` shell:

> 你可以自定义GDB来使用vi编辑器，你可以使用sh shell中的这些命令：

::: smallexample

```bash
EDITOR=/usr/bin/vi
export EDITOR
gdb …
```

:::

or in the `csh` shell,

::: smallexample

```bash
setenv EDITOR /usr/bin/vi
gdb …
```

:::

::: footnote

---

#### Footnotes

### [(10)](#DOCF10)


The only restriction is that your editor (say `ex`), recognizes the following command-line syntax:

> 只有一个限制，就是您的编辑器（比如 `ex`）能够识别以下命令行语法：

::: smallexample

```bash
ex +number file
```

:::


The optional numeric value +`number` specifies the number of the line in the file where to start editing.

> 可选的数字值+`number`指定文件中开始编辑的行号。
:::

---

::: header
Next: [Search](Search.html#Search)]
:::
