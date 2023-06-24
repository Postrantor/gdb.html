---
tip: translate by openai@2023-06-23 21:23:31
...
---
description: Frame Info (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Frame Info (Debugging with GDB)
lang: en
resource-type: document
title: Frame Info (Debugging with GDB)
---
::: header
Next: [Frame Apply](Frame-Apply.html#Frame-Apply)]
:::

---

### 8.4 Information About a Frame


There are several other commands to print information about the selected stack frame.

> 有几个其他的命令可以打印关于所选择的堆栈帧的信息。

`frame`
`f`


:   When used without any argument, this command does not change which frame is selected, but prints a brief description of the currently selected stack frame. It can be abbreviated `f`. With an argument, this command is used to select a stack frame. See [Selecting a Frame](Selection.html#Selection).

> 当没有任何参数使用时，此命令不会改变所选择的帧，但会打印当前所选堆栈帧的简要描述。它可以简写为“f”。带参数时，此命令用于选择堆栈帧。请参阅[选择帧](Selection.html#Selection)。

```

```

`info frame`
`info f`


:   This command prints a verbose description of the selected stack frame, including:

> 此命令会打印出所选堆栈帧的详细描述，包括：

```
-   the address of the frame
-   the address of the next frame down (called by this frame)
-   the address of the next frame up (caller of this frame)
-   the language in which the source code corresponding to this frame is written
-   the address of the frame's arguments
-   the address of the frame's local variables
-   the program counter saved in it (the address of execution in the caller frame)
-   which registers were saved in the frame

The verbose description is useful when something has gone wrong that has made the stack format fail to fit the usual conventions.
```

`info frame [ frame-selection-spec ]`
`info f [ frame-selection-spec ]`


:   Print a verbose description of the frame selected by `frame-selection-spec` is the same as for the `frame` command (see [Selecting a Frame](Selection.html#Selection)). The selected frame remains unchanged by this command.

> 打印出由`frame-selection-spec`选择的框架的详细描述与`frame`命令相同（参见[选择框架](Selection.html#Selection)）。此命令不会改变所选择的框架。

```

```

`info args [-q]`

:   Print the arguments of the selected frame, each on a separate line.

```
The optional flag '`-q`', disables printing header information and messages explaining why no argument have been printed.
```

`info args [-q] [-t type_regexp] [regexp]`


:   Like [info args], but only print the arguments selected with the provided regexp(s).

> 像[info args]一样，但只打印使用提供的正则表达式选择的参数。

```
If `regexp`.

If `type_regexp` contains space(s), it should be enclosed in quote characters. If needed, use backslash to escape the meaning of special characters or quotes.

If both `regexp`.
```

`info locals [-q]`

:

```
Print the local variables of the selected frame, each on a separate line. These are all variables (declared either static or automatic) accessible at the point of execution of the selected frame.

The optional flag '`-q`', disables printing header information and messages explaining why no local variables have been printed.
```

`info locals [-q] [-t type_regexp] [regexp]`


:   Like [info locals], but only print the local variables selected with the provided regexp(s).

> 像[info locals]一样，但只打印使用提供的正则表达式选择的局部变量。

```
If `regexp`.

If `type_regexp` contains space(s), it should be enclosed in quote characters. If needed, use backslash to escape the meaning of special characters or quotes.

If both `regexp`.

The command [info locals -q -t `type_regexp`. For example, your program might use Resource Acquisition Is Initialization types (RAII) such as `lock_something_t`: each local variable of type `lock_something_t` automatically places a lock that is destroyed when the variable goes out of scope. You can then list all acquired locks in your program by doing

::: smallexample
``` smallexample
thread apply all -s frame apply all -s info locals -q -t lock_something_t
```

:::

or the equivalent shorter form

::: smallexample

```bash
tfaas i lo -q -t lock_something_t
```

:::

```

---

::: header
Next: [Frame Apply](Frame-Apply.html#Frame-Apply)]
:::
```
