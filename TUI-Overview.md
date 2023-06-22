---
description: TUI Overview (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: TUI Overview (Debugging with GDB)
lang: en
resource-type: document
title: TUI Overview (Debugging with GDB)
---
::: header
Next: [TUI Keys](TUI-Keys.html#TUI-Keys)]
:::

---

### 25.1 TUI Overview

In TUI mode, [GDB] can display several text windows:

*command*

:   This window is the [GDB] input is still managed using readline.

*source*

:   The source window shows the source file of the program. The current line and active breakpoints are displayed in this window.

*assembly*

:   The assembly window shows the disassembly output of the program.

*register*

:   This window shows the processor registers. Registers are highlighted when their values change.

The source and assembly windows show the current program position by highlighting the current line and marking it with a '`>`' marker. By default, source and assembly code styling is disabled for the highlighted text, but you can enable it with the `set style tui-current-position on` command. See [Output Styling](Output-Styling.html#Output-Styling).

Breakpoints are indicated with two markers. The first marker indicates the breakpoint type:

`B`

:   Breakpoint which was hit at least once.

`b`

:   Breakpoint which was never hit.

`H`

:   Hardware breakpoint which was hit at least once.

`h`

:   Hardware breakpoint which was never hit.

The second marker indicates whether the breakpoint is enabled or not:

`+`

:   Breakpoint is enabled.

`-`

:   Breakpoint is disabled.

The source, assembly and register windows are updated when the current thread changes, when the frame changes, or when the program counter changes.

These windows are not all visible at the same time. The command window is always visible. The others can be arranged in several layouts:

- source only,
- assembly only,
- source and assembly,
- source and registers, or
- assembly and registers.

These are the standard layouts, but other layouts can be defined.

A status line above the command window shows the following information:

*target*

:   Indicates the current [GDB] target. (see [Specifying a Debugging Target](Targets.html#Targets)).

*process*

:   Gives the current process or thread number. When no process is being debugged, this field is set to `No process`.

*function*

:   Gives the current function name for the selected frame. The name is demangled if demangling is turned on (see [Print Settings](Print-Settings.html#Print-Settings)). When there is no symbol corresponding to the current program counter, the string `??` is displayed.

*line*

:   Indicates the current line number for the selected frame. When the current line number is not known, the string `??` is displayed.

*pc*

:   Indicates the current program counter address.

---

::: header
Next: [TUI Keys](TUI-Keys.html#TUI-Keys)]
:::
