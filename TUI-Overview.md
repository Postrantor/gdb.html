---
tip: translate by openai@2023-06-24 04:16:31
...
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

> 窗口源显示程序的源文件。当前行和活动断点在此窗口中显示。

*assembly*

:   The assembly window shows the disassembly output of the program.

*register*


:   This window shows the processor registers. Registers are highlighted when their values change.

> 这个窗口显示处理器寄存器。当寄存器的值发生变化时，它们会被突出显示。


The source and assembly windows show the current program position by highlighting the current line and marking it with a '`>`' marker. By default, source and assembly code styling is disabled for the highlighted text, but you can enable it with the `set style tui-current-position on` command. See [Output Styling](Output-Styling.html#Output-Styling).

> 源码窗口和汇编窗口通过突出显示当前行并使用'>'标记来显示当前程序位置。默认情况下，突出显示的文本的源代码和汇编代码样式被禁用，但可以使用`set style tui-current-position on`命令来启用它。参见[输出样式](Output-Styling.html#Output-Styling)。


Breakpoints are indicated with two markers. The first marker indicates the breakpoint type:

> 断点用两个标记表示。第一个标记指示断点类型：

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

> 当当前线程发生变化、当帧发生变化或当程序计数器发生变化时，源窗口、装配窗口和寄存器窗口都会更新。


These windows are not all visible at the same time. The command window is always visible. The others can be arranged in several layouts:

> 这些窗口不能同时可见。命令窗口总是可见的。其他窗口可以按多种布局排列。

- source only,
- assembly only,
- source and assembly,
- source and registers, or
- assembly and registers.

These are the standard layouts, but other layouts can be defined.

A status line above the command window shows the following information:

*target*


:   Indicates the current [GDB] target. (see [Specifying a Debugging Target](Targets.html#Targets)).

> :表示当前的[GDB]目标（参见[指定调试目标](Targets.html#Targets)）。

*process*


:   Gives the current process or thread number. When no process is being debugged, this field is set to `No process`.

> 当前进程或线程号。 当没有进程被调试时，此字段设置为“无进程”。

*function*


:   Gives the current function name for the selected frame. The name is demangled if demangling is turned on (see [Print Settings](Print-Settings.html#Print-Settings)). When there is no symbol corresponding to the current program counter, the string `??` is displayed.

> 给出所选择帧的当前函数名称。如果解码已打开（请参见[打印设置] (Print-Settings.html#Print-Settings)），则名称将被解码。如果没有与当前程序计数器对应的符号，则显示字符串“??”。

*line*


:   Indicates the current line number for the selected frame. When the current line number is not known, the string `??` is displayed.

> `:`表示所选帧的当前行号。当当前行号未知时，将显示字符串`??`。

*pc*

:   Indicates the current program counter address.

---

::: header
Next: [TUI Keys](TUI-Keys.html#TUI-Keys)]
:::
