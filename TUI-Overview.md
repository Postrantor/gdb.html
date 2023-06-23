---
tip: translate by openai@2023-06-23 14:53:45
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

> 在TUI模式下，[GDB]可以显示多个文本窗口：

*command*


:   This window is the [GDB] input is still managed using readline.

> 这个窗口是GDB输入仍然使用readline管理。

*source*


:   The source window shows the source file of the program. The current line and active breakpoints are displayed in this window.

> 窗口源显示程序的源文件。当前行和活动断点在此窗口中显示。

*assembly*


:   The assembly window shows the disassembly output of the program.

> 程序集窗口显示程序的反汇编输出。

*register*


:   This window shows the processor registers. Registers are highlighted when their values change.

> 这个窗口显示处理器寄存器。当寄存器的值发生变化时，它们会被突出显示。


The source and assembly windows show the current program position by highlighting the current line and marking it with a '`>`' marker. By default, source and assembly code styling is disabled for the highlighted text, but you can enable it with the `set style tui-current-position on` command. See [Output Styling](Output-Styling.html#Output-Styling).

> 源代码和汇编窗口通过突出显示当前行并用“>”标记来显示当前程序位置。默认情况下，突出显示的文本的源代码和汇编代码样式被禁用，但是可以通过`set style tui-current-position on`命令来启用它。请参见[输出样式](Output-Styling.html#Output-Styling)。


Breakpoints are indicated with two markers. The first marker indicates the breakpoint type:

> 断点用两个标记表示。第一个标记表示断点类型。

`B`


:   Breakpoint which was hit at least once.

> 至少被击中过一次的断点。

`b`


:   Breakpoint which was never hit.

> 断点从未被触发。

`H`


:   Hardware breakpoint which was hit at least once.

> 硬件断点至少被触发过一次。

`h`


:   Hardware breakpoint which was never hit.

> 硬件断点从未被触发。


The second marker indicates whether the breakpoint is enabled or not:

> 第二个标记表示断点是否启用。

`+`


:   Breakpoint is enabled.

> 断点已启用。

`-`


:   Breakpoint is disabled.

> 断点已禁用。


The source, assembly and register windows are updated when the current thread changes, when the frame changes, or when the program counter changes.

> 当当前线程改变、帧改变或程序计数器改变时，源、组装和寄存器窗口将被更新。


These windows are not all visible at the same time. The command window is always visible. The others can be arranged in several layouts:

> 这些窗口不能同时可见。命令窗口总是可见的。其他窗口可以按几种布局排列。

- source only,
- assembly only,
- source and assembly,
- source and registers, or
- assembly and registers.


These are the standard layouts, but other layouts can be defined.

> 这些是标准布局，但也可以定义其他布局。


A status line above the command window shows the following information:

> 命令窗口上方的状态行显示以下信息：

*target*


:   Indicates the current [GDB] target. (see [Specifying a Debugging Target](Targets.html#Targets)).

> : 指示当前的[GDB]目标（参见[指定调试目标](Targets.html#Targets)）。

*process*


:   Gives the current process or thread number. When no process is being debugged, this field is set to `No process`.

> 给出当前进程或线程号码。当没有进程被调试时，此字段设置为“无进程”。

*function*


:   Gives the current function name for the selected frame. The name is demangled if demangling is turned on (see [Print Settings](Print-Settings.html#Print-Settings)). When there is no symbol corresponding to the current program counter, the string `??` is displayed.

> 给出当前选定帧的函数名称。如果开启了解码（参见[打印设置](Print-Settings.html#Print-Settings)），则会对名称进行解码。当没有与当前程序计数器相对应的符号时，将显示字符串“??”。

*line*


:   Indicates the current line number for the selected frame. When the current line number is not known, the string `??` is displayed.

> `:`表示所选框架的当前行号。当当前行号未知时，将显示字符串“??”。

*pc*


:   Indicates the current program counter address.

> 表示当前程序计数器地址。

---

::: header
Next: [TUI Keys](TUI-Keys.html#TUI-Keys)]
:::
