---
description: gdb.prompt (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: gdb.prompt (Debugging with GDB)
lang: en
resource-type: document
title: gdb.prompt (Debugging with GDB)
---
::: header
Previous: [gdb.types](gdb_002etypes.html#gdb_002etypes)]
:::

---

#### 23.3.4.3 gdb.prompt

This module provides a method for prompt value-substitution.

`substitute_prompt (string)`

:   Return `string`" immediately following the escape sequence.

```
The escape sequences you can pass to this function are:

`\\`

:   Substitute a backslash.

`\e`

:   Substitute an ESC character.

`\f`

:   Substitute the selected frame; an argument names a frame parameter.

`\n`

:   Substitute a newline.

`\p`

:   Substitute a parameter's value; the argument names the parameter.

`\r`

:   Substitute a carriage return.

`\t`

:   Substitute the selected thread; an argument names a thread parameter.

`\v`

:   Substitute the version of GDB.

`\w`

:   Substitute the current working directory.

`\[`

:   Begin a sequence of non-printing characters. These sequences are typically used with the ESC character, and are not counted in the string length. Example: "\\\[\\e\[0;34m\\](gdb)\\\[\\e\[0m\\]" will return a blue-colored "(gdb)" prompt where the length is five.

`]`

:   End a sequence of non-printing characters.

For example:

::: smallexample
``` smallexample
substitute_prompt ("frame: \f, args: \p")
```

:::

will return the string:

::: smallexample

```bash
"frame: main, args: scalars"
```

:::

```
```
