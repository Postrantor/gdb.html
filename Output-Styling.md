---
tip: translate by openai@2023-06-24 00:51:51
...
---
description: Output Styling (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Output Styling (Debugging with GDB)
lang: en
resource-type: document
title: Output Styling (Debugging with GDB)
---
::: header
Next: [Numbers](Numbers.html#Numbers)]
:::

---

### 22.5 Output Styling


[GDB] can style its output on a capable terminal. This is enabled by default on most systems, but disabled by default when in batch mode (see [Mode Options](Mode-Options.html#Mode-Options)). Various style settings are available; and styles can also be disabled entirely.

> [GDB] 可以在兼容的终端上调整其输出的样式。在大多数系统中，这默认是启用的，但是在批处理模式下默认是禁用的（参见[模式选项](Mode-Options.html#Mode-Options)）。可用的样式设置有很多；也可以完全禁用样式。

`set style enabled ‘on|off’`


:   Enable or disable all styling. The default is host-dependent, with most hosts defaulting to '`on`'.

> 启用或禁用所有样式。默认值取决于主机，大多数主机的默认值为“开”。

`show style enabled`

:   Show the current state of styling.

`set style sources ‘on|off’`


:   Enable or disable source code styling. This affects whether source code, such as the output of the `list` command, is styled. The default is '`on`.

> 启用或禁用源代码样式。 这会影响源代码的样式，例如`list`命令的输出。 默认为'`on`。

```
There are two ways that highlighting can be done. First, if [GDB] was configured with Python scripting support, and if the Python Pygments package is available, then it will be used.
```

`show style sources`

:   Show the current state of source code styling.

`set style tui-current-position ‘on|off’`


:   Enable or disable styling of the source and assembly code highlighted by the TUI's current position indicator. The default is '`off` Text User Interface](TUI.html#TUI).

> 启用或禁用TUI当前位置指示器高亮显示的源代码和汇编代码的样式。默认为'关'文本用户界面（TUI）。

`show style tui-current-position`


:   Show whether the source and assembly code highlighted by the TUI's current position indicator is styled.

> 请帮助我翻译：检查TUI当前位置指示器高亮显示的源代码和汇编代码是否有样式。

```

```

`set style disassembler enabled ‘on|off’`


:   Enable or disable disassembler styling. This affects whether disassembler output, such as the output of the `disassemble` command, is styled. Disassembler styling only works if styling in general is enabled (with `set style enabled on`), and if a source highlighting library is available to [GDB].

> 启用或禁用反汇编器样式。这会影响反汇编器输出，例如`disassemble`命令的输出，是否受到样式的影响。只有在一般样式启用（使用`set style enabled on`）并且可以向[GDB]提供源代码高亮库时，反汇编器样式才有效。

```
The two source highlighting libraries that [GDB]'s builtin disassembler, or the Python Pygments package.

[GDB]'s first choice will be to use the builtin disassembler for styling, this usually provides better results, being able to style different types of instruction operands differently. However, the builtin disassembler is not able to style all architectures.

For architectures that the builtin disassembler is unable to style, [GDB] must be built with Python support, and the Pygments package must be installed.

If neither of these options are available then [GDB]'.

To discover if the current architecture supports styling using the builtin disassembler library see [[maint show libopcodes-styling enabled]](Maintenance-Commands.html#maint_005flibopcodes_005fstyling).
```

`show style disassembler enabled`

:   Show the current state of disassembler styling.


Subcommands of `set style` control specific forms of styling. These subcommands all follow the same pattern: each style-able object can be styled with a foreground color, a background color, and an intensity.

> `set style` 的子命令控制特定形式的样式。这些子命令遵循相同的模式：每个可样式化的对象都可以使用前景颜色、背景颜色和强度进行样式化。


For example, the style of file names can be controlled using the `set style filename` group of commands:

> 例如，可以使用`set style filename`组命令来控制文件名的样式：

`set style filename background color`

:   Set the background to `color`'.

`set style filename foreground color`

:   Set the foreground to `color`'.

`set style filename intensity value`

:   Set the intensity to `value`'.


The `show style` command and its subcommands are styling a style name in their output using its own style. So, use `show style` to see the complete list of styles, their characteristics and the visual aspect of each style.

> 命令 `show style` 及其子命令可以使用自己的样式对样式名称进行样式化输出。因此，使用 `show style` 命令可以查看完整的样式列表、它们的特性以及每种样式的视觉外观。

The style-able objects are:

`filename`


:   Control the styling of file names and URLs. By default, this style's foreground color is green.

> 控制文件名和URL的样式。默认情况下，该样式的前景色为绿色。

`function`


:   Control the styling of function names. These are managed with the `set style function` family of commands. By default, this style's foreground color is yellow.

> 控制函数名的样式。这些使用`set style function`系列命令进行管理。默认情况下，此样式的前景色为黄色。

```
This style is also used for symbol names in styled disassembler output if [GDB]](#style_005fdisassembler_005fenabled)).
```

`variable`


:   Control the styling of variable names. These are managed with the `set style variable` family of commands. By default, this style's foreground color is cyan.

> 控制变量名的样式。这些由`set style variable`命令族管理。默认情况下，这种样式的前景颜色为青色。

`address`


:   Control the styling of addresses. These are managed with the `set style address` family of commands. By default, this style's foreground color is blue.

> 控制地址的样式。这些是用`set style address`系列命令管理的。默认情况下，该样式的前景色为蓝色。

```
This style is also used for addresses in styled disassembler output if [GDB]](#style_005fdisassembler_005fenabled)).
```

`version`

:   Control the styling of [GDB] starts up.

```
In order to control how [GDB] styles the version number at startup, add the `set style version` family of commands to the early initialization command file (see [Initialization Files](Initialization-Files.html#Initialization-Files)).
```

`title`


:   Control the styling of titles. These are managed with the `set style title` family of commands. By default, this style's intensity is bold. Commands are using the title style to improve the readability of large output. For example, the commands `apropos` and `help` are using the title style for the command names.

> 控制标题的样式。这些是使用`set style title`系列命令管理的。默认情况下，这种样式的强度为粗体。命令使用标题样式来提高大量输出的可读性。例如，`apropos`和`help`命令使用标题样式来显示命令名称。

`highlight`


:   Control the styling of highlightings. These are managed with the `set style highlight` family of commands. By default, this style's foreground color is red. Commands are using the highlight style to draw the user attention to some specific parts of their output. For example, the command `apropos -v REGEXP` uses the highlight style to mark the documentation parts matching `regexp`.

> 控制高亮的样式。这些可以使用`set style highlight`系列命令来管理。默认情况下，这种样式的前景色是红色的。命令使用高亮样式来吸引用户的注意力，聚焦到输出的某些特定部分。例如，命令`apropos -v REGEXP`使用高亮样式来标记与`regexp`匹配的文档部分。

`metadata`


:   Control the styling of data annotations added by [GDB]' annotations for optimized-out values in displaying stack frame information in backtraces (see [Backtrace](Backtrace.html#Backtrace)), etc.

> 控制[GDB]添加的数据注释在显示堆栈帧信息（参见[Backtrace](Backtrace.html#Backtrace)）等的优化输出值中的样式。

`tui-border`


:   Control the styling of the TUI border. Note that, unlike other styling options, only the color of the border can be controlled via `set style`. This was done for compatibility reasons, as TUI controls to set the border's intensity predated the addition of general styling to [GDB]. See [TUI Configuration](TUI-Configuration.html#TUI-Configuration).

> 控制TUI边框的样式。请注意，与其他样式选项不同，只能通过“set style”来控制边框的颜色。这是为了兼容性的原因，因为TUI控件设置边框强度的功能早于向[GDB]添加一般样式。请参阅[TUI配置](TUI-Configuration.html#TUI-Configuration)。

`tui-active-border`


:   Control the styling of the active TUI border; that is, the TUI window that has the focus.

> 控制活动TUI边框的样式，即具有焦点的TUI窗口。

`disassembler comment`


:   Control the styling of comments in the disassembler output. These are managed with the `set style disassembler comment` family of commands. This style is only used when [GDB]](#style_005fdisassembler_005fenabled)). By default, this style's intensity is dim, and its foreground color is white.

> 控制反汇编输出中注释的样式。这些由`set style disassembler comment`系列命令管理。只有在[GDB]](#style_005fdisassembler_005fenabled))时才使用这种样式。默认情况下，此样式的强度为暗，其前景色为白色。

`disassembler immediate`


:   Control the styling of numeric operands in the disassembler output. These are managed with the `set style disassembler immediate` family of commands. This style is not used for instruction operands that represent addresses, in that case the '`disassembler address` is styling using its builtin disassembler library. By default, this style's foreground color is blue.

> 控制反汇编器输出中的数字操作数的样式。这些由`set style disassembler immediate`系列命令管理。此样式不适用于表示地址的指令操作数，在这种情况下，使用内置反汇编库对'`disassembler address`样式进行样式设置。默认情况下，此样式的前景色为蓝色。

`disassembler address`


:   Control the styling of address operands in the disassembler output. This is an alias for the '`address`' style.

> 控制反汇编输出中地址操作数的样式。这是对 '`address`' 样式的别名。

`disassembler symbol`


:   Control the styling of symbol names in the disassembler output. This is an alias for the '`function`' style.

> 控制反汇编输出中符号名称的样式。这是“function”样式的别名。

`disassembler mnemonic`


:   Control the styling of instruction mnemonics in the disassembler output. These are managed with the `set style disassembler mnemonic` family of commands. This style is also used for assembler directives, e.g. `.byte`, `.word`, etc. This style is only used when [GDB] is styling using its builtin disassembler library. By default, this style's foreground color is green.

> 控制反汇编输出中指令指示符的样式。这些是用`set style disassembler mnemonic`系列命令管理的。这种样式也用于汇编指令，例如`.byte`，`.word`等。只有在[GDB]使用内置的反汇编库样式化时，才使用此样式。默认情况下，此样式的前景色为绿色。

`disassembler register`


:   Control the styling of register operands in the disassembler output. These are managed with the `set style disassembler register` family of commands. This style is only used when [GDB] is styling using its builtin disassembler library. By default, this style's foreground color is red.

> 在反汇编器输出中控制注册操作数的样式。这些由`set style disassembler register`系列命令管理。当[GDB]使用其内置的反汇编器库进行样式控制时，才使用此样式。默认情况下，此样式的前景色为红色。

---

::: header
Next: [Numbers](Numbers.html#Numbers)]
:::
