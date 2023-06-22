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

`edit locspec`

:   Edit the source file of the code location that results from resolving `locspec`. Editing starts at the source file and source line `locspec` resolves to. See [Location Specifications](Location-Specifications.html#Location-Specifications), for all the possible forms of the `locspec` argument.

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

::: smallexample

```bash
ex +number file
```

:::

The optional numeric value +`number` specifies the number of the line in the file where to start editing.
:::

---

::: header
Next: [Search](Search.html#Search)]
:::
