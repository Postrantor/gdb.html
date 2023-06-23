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

`set style enabled ‘on|off’`

:   Enable or disable all styling. The default is host-dependent, with most hosts defaulting to '`on`'.

`show style enabled`

:   Show the current state of styling.

`set style sources ‘on|off’`

:   Enable or disable source code styling. This affects whether source code, such as the output of the `list` command, is styled. The default is '`on`.

```
There are two ways that highlighting can be done. First, if [GDB] was configured with Python scripting support, and if the Python Pygments package is available, then it will be used.
```

`show style sources`

:   Show the current state of source code styling.

`set style tui-current-position ‘on|off’`

:   Enable or disable styling of the source and assembly code highlighted by the TUI's current position indicator. The default is '`off` Text User Interface](TUI.html#TUI).

`show style tui-current-position`

:   Show whether the source and assembly code highlighted by the TUI's current position indicator is styled.

```

```

`set style disassembler enabled ‘on|off’`

:   Enable or disable disassembler styling. This affects whether disassembler output, such as the output of the `disassemble` command, is styled. Disassembler styling only works if styling in general is enabled (with `set style enabled on`), and if a source highlighting library is available to [GDB].

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

For example, the style of file names can be controlled using the `set style filename` group of commands:

`set style filename background color`

:   Set the background to `color`'.

`set style filename foreground color`

:   Set the foreground to `color`'.

`set style filename intensity value`

:   Set the intensity to `value`'.

The `show style` command and its subcommands are styling a style name in their output using its own style. So, use `show style` to see the complete list of styles, their characteristics and the visual aspect of each style.

The style-able objects are:

`filename`

:   Control the styling of file names and URLs. By default, this style's foreground color is green.

`function`

:   Control the styling of function names. These are managed with the `set style function` family of commands. By default, this style's foreground color is yellow.

```
This style is also used for symbol names in styled disassembler output if [GDB]](#style_005fdisassembler_005fenabled)).
```

`variable`

:   Control the styling of variable names. These are managed with the `set style variable` family of commands. By default, this style's foreground color is cyan.

`address`

:   Control the styling of addresses. These are managed with the `set style address` family of commands. By default, this style's foreground color is blue.

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

`highlight`

:   Control the styling of highlightings. These are managed with the `set style highlight` family of commands. By default, this style's foreground color is red. Commands are using the highlight style to draw the user attention to some specific parts of their output. For example, the command `apropos -v REGEXP` uses the highlight style to mark the documentation parts matching `regexp`.

`metadata`

:   Control the styling of data annotations added by [GDB]' annotations for optimized-out values in displaying stack frame information in backtraces (see [Backtrace](Backtrace.html#Backtrace)), etc.

`tui-border`

:   Control the styling of the TUI border. Note that, unlike other styling options, only the color of the border can be controlled via `set style`. This was done for compatibility reasons, as TUI controls to set the border's intensity predated the addition of general styling to [GDB]. See [TUI Configuration](TUI-Configuration.html#TUI-Configuration).

`tui-active-border`

:   Control the styling of the active TUI border; that is, the TUI window that has the focus.

`disassembler comment`

:   Control the styling of comments in the disassembler output. These are managed with the `set style disassembler comment` family of commands. This style is only used when [GDB]](#style_005fdisassembler_005fenabled)). By default, this style's intensity is dim, and its foreground color is white.

`disassembler immediate`

:   Control the styling of numeric operands in the disassembler output. These are managed with the `set style disassembler immediate` family of commands. This style is not used for instruction operands that represent addresses, in that case the '`disassembler address` is styling using its builtin disassembler library. By default, this style's foreground color is blue.

`disassembler address`

:   Control the styling of address operands in the disassembler output. This is an alias for the '`address`' style.

`disassembler symbol`

:   Control the styling of symbol names in the disassembler output. This is an alias for the '`function`' style.

`disassembler mnemonic`

:   Control the styling of instruction mnemonics in the disassembler output. These are managed with the `set style disassembler mnemonic` family of commands. This style is also used for assembler directives, e.g. `.byte`, `.word`, etc. This style is only used when [GDB] is styling using its builtin disassembler library. By default, this style's foreground color is green.

`disassembler register`

:   Control the styling of register operands in the disassembler output. These are managed with the `set style disassembler register` family of commands. This style is only used when [GDB] is styling using its builtin disassembler library. By default, this style's foreground color is red.

---

::: header
Next: [Numbers](Numbers.html#Numbers)]
:::
