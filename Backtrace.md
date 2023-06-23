---
tip: translate by openai@2023-06-23 12:00:40
...
---
description: Backtrace (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Backtrace (Debugging with GDB)
lang: en
resource-type: document
title: Backtrace (Debugging with GDB)
-------------------------------------

::: header
Next: [Selection](Selection.html#Selection)]
:::

---

### 8.2 Backtraces

A backtrace is a summary of how your program got where it is. It shows one line per frame, for many frames, starting with the currently executing frame (frame zero), followed by its caller (frame one), and on up the stack.

> 回溯是您的程序到达当前位置的概要。它显示多个帧的每个帧一行，从当前执行帧（帧零）开始，其接着是调用者（帧一），然后一直上溯到堆栈。

To print a backtrace of the entire stack, use the `backtrace` command, or its alias `bt`. This command will print one line per frame for frames in the stack. By default, all stack frames are printed. You can stop the backtrace at any time by typing the system interrupt character, normally [Ctrl-c].

> 要打印整个堆栈跟踪，请使用 `backtrace` 命令或其别名 `bt`。此命令将为堆栈中的每个帧打印一行。默认情况下，将打印所有堆栈帧。您可以随时通过输入系统中断字符（通常为[Ctrl-c]）来停止回溯。

`backtrace [option]… [qualifier]… [count]`
`bt [option]… [qualifier]… [count]`

:   Print the backtrace of the entire stack.

> 打印整个堆栈跟踪。

```
The optional `count` can be one of the following:

`n`\
`n`

:   Print only the innermost `n` is a positive number.

`-n`\
`-n`

:   Print only the outermost `n` is a positive number.

Options:

`-full`

:   Print the values of the local variables also. This can be combined with the optional `count` to limit the number of frames shown.

`-no-filters`

:   Do not run Python frame filters on this backtrace. See [Frame Filter API](Frame-Filter-API.html#Frame-Filter-API), for more information. Additionally use [disable frame-filter all](Frame-Filter-Management.html#disable-frame_002dfilter-all) to turn off all frame filters. This is only relevant when [GDB] has been configured with `Python` support.

`-hide`

:   A Python frame filter might decide to "elide" some frames. Normally such elided frames are still printed, but they are indented relative to the filtered frames that cause them to be elided. The `-hide` option causes elided frames to not be printed at all.

The `backtrace` command also supports a number of options that allow overriding relevant global print settings as set by `set backtrace` and `set print` subcommands:

`-past-main [on`\|`off`]

:   Set whether backtraces should continue past `main`. Related setting: [set backtrace past-main](#set-backtrace-past_002dmain).

`-past-entry [on`\|`off`]

:   Set whether backtraces should continue past the entry point of a program. Related setting: [set backtrace past-entry](#set-backtrace-past_002dentry).

`-entry-values no`\|`only`\|`preferred`\|`if-needed`\|`both`\|`compact`\|`default`

:   Set printing of function arguments at function entry. Related setting: [set print entry-values](Print-Settings.html#set-print-entry_002dvalues).

`-frame-arguments all`\|`scalars`\|`none`

:   Set printing of non-scalar frame arguments. Related setting: [set print frame-arguments](Print-Settings.html#set-print-frame_002darguments).

`-raw-frame-arguments [on`\|`off`]

:   Set whether to print frame arguments in raw form. Related setting: [set print raw-frame-arguments](Print-Settings.html#set-print-raw_002dframe_002darguments).

`-frame-info auto`\|`source-line`\|`location`\|`source-and-location`\|`location-and-address`\|`short-location`

:   Set printing of frame information. Related setting: [set print frame-info](Print-Settings.html#set-print-frame_002dinfo).

The optional `qualifier` is maintained for backward compatibility. It can be one of the following:

`full`

:   Equivalent to the `-full` option.

`no-filters`

:   Equivalent to the `-no-filters` option.

`hide`

:   Equivalent to the `-hide` option.
```

The names `where` and `info stack` (abbreviated `info s`) are additional aliases for `backtrace`.

> `where` 和 `info stack`（缩写为 `info s`）是 `backtrace` 的其他别名。

In a multi-threaded program, [GDB] will display the backtrace for all the threads; this is handy when you debug a core dump of a multi-threaded program.

> 在多线程程序中，[GDB]会显示所有线程的回溯；当你调试多线程程序的核心转储时，这很方便。

Each line in the backtrace shows the frame number and the function name. The program counter value is also shown---unless you use `set print address off`. The backtrace also shows the source file name and line number, as well as the arguments to the function. The program counter value is omitted if it is at the beginning of the code for that line number.

> 每一行回溯显示框架号和函数名。也会显示程序计数器的值---除非你使用 `set print address off`。回溯也会显示源文件名和行号，以及函数的参数。如果程序计数器的值在该行号的代码开头，则会省略程序计数器的值。

Here is an example of a backtrace. It was made with the command '`bt 3`', so it shows the innermost three frames.

> 这里是一个回溯的例子。它是用命令 'bt 3' 制作的，因此它显示了最内层的三个帧。

::: smallexample

```bash
#0  m4_traceon (obs=0x24eb0, argc=1, argv=0x2b8c8)
    at builtin.c:993
#1  0x6e38 in expand_macro (sym=0x2b600, data=...) at macro.c:242
#2  0x6840 in expand_token (obs=0x0, t=177664, td=0xf7fffb08)
    at macro.c:71
(More stack frames follow...)
```

:::

The display for frame zero does not begin with a program counter value, indicating that your program has stopped at the beginning of the code for line `993` of `builtin.c`.

> 显示帧零不以程序计数器值开始，表明您的程序已停止在 builtin.c 的第 993 行代码的开始处。

The value of parameter `data` in frame 1 has been replaced by `…`. By default, [GDB] (see [Print Settings](Print-Settings.html#Print-Settings)) controls what frame information is printed.

> 参数 `data` 在帧 1 中的值已被替换为 `…`。 默认情况下，[GDB]（参见[打印设置]（Print-Settings.html#Print-Settings））控制打印哪些帧信息。

If your program was compiled with optimizations, some compilers will optimize away arguments passed to functions if those arguments are never used after the call. Such optimizations generate code that passes arguments through registers, but doesn't store those arguments in the stack frame. [GDB] has no way of displaying such arguments in stack frames other than the innermost one. Here's what such a backtrace might look like:

> 如果您的程序使用了优化，一些编译器会在调用函数后没有使用参数时优化掉这些参数。这种优化会生成通过寄存器传递参数的代码，但不会将这些参数存储在堆栈帧中。[GDB]无法在除最内层之外的堆栈帧中显示这些参数。这就是回溯可能看起来像的：

::: smallexample

```bash
#0  m4_traceon (obs=0x24eb0, argc=1, argv=0x2b8c8)
    at builtin.c:993
#1  0x6e38 in expand_macro (sym=<optimized out>) at macro.c:242
#2  0x6840 in expand_token (obs=0x0, t=<optimized out>, td=0xf7fffb08)
    at macro.c:71
(More stack frames follow...)
```

:::

The values of arguments that were not saved in their stack frames are shown as '`<optimized out>`'.

> 参数的值没有保存在它们的堆栈帧中时，会显示为“< 优化掉 >”。

If you need to display the values of such optimized-out arguments, either deduce that from other variables whose values depend on the one you are interested in, or recompile without optimizations.

> 如果您需要显示优化掉的参数的值，可以从其他变量的值中推断出您感兴趣的值，或者重新编译而不使用优化。

Most programs have a standard user entry point---a place where system libraries and startup code transition into user code. For C this is `main`[^9^](#FOOT9) finds the entry function in a backtrace it will terminate the backtrace, to avoid tracing into highly system-specific (and generally uninteresting) code.

> 大多数程序都有一个标准的用户入口点——一个系统库和启动代码转换为用户代码的地方。对于 C 来说，这是 `main`[^9^]（#FOOT9），它可以在回溯中找到入口函数，以避免跟踪进入高度系统特定（通常也不太有趣）的代码。

If you need to examine the startup code, or limit the number of levels in a backtrace, you can change this behavior:

> 如果您需要检查启动代码或限制回溯中的层数，您可以更改此行为：

`set backtrace past-main`
`set backtrace past-main on`

:

```
Backtraces will continue past the user entry point.
```

`set backtrace past-main off`

:   Backtraces will stop when they encounter the user entry point. This is the default.

> 回溯将在遇到用户入口点时停止。这是默认设置。

`show backtrace past-main`

:

```
Display the current user entry point backtrace policy.
```

`set backtrace past-entry`
`set backtrace past-entry on`

:

```
Backtraces will continue past the internal entry point of an application. This entry point is encoded by the linker when the application is built, and is likely before the user entry point `main` (or equivalent) is called.
```

`set backtrace past-entry off`

:   Backtraces will stop when they encounter the internal entry point of an application. This is the default.

> 回溯将在遇到应用程序的内部入口点时停止。这是默认设置。

`show backtrace past-entry`

:   Display the current internal entry point backtrace policy.

> 显示当前内部入口点回溯策略。

`set backtrace limit n`
`set backtrace limit 0`
`set backtrace limit unlimited`

:

```
Limit the backtrace to `n` levels. A value of `unlimited` or zero means unlimited levels.
```

`show backtrace limit`

:   Display the current limit on backtrace levels.

> 顯示當前的回溯級別限制。

You can control how file names are displayed.

> 你可以控制文件名的显示方式。

`set filename-display`
`set filename-display relative`

:

```
Display file names relative to the compilation directory. This is the default.
```

`set filename-display basename`

:   Display only basename of a filename.

> 只显示文件名的基本名称。

`set filename-display absolute`

:   Display an absolute filename.

> 显示一个绝对文件名。

`show filename-display`

:   Show the current way to display filenames.

> 显示当前文件名的显示方式。

::: footnote

---

#### Footnotes

### [(9)](#DOCF9)

Note that embedded programs (the so-called "free-standing" environment) are not required to have a `main` function as the entry point. They could even have multiple entry points.
:::

---

::: header
Next: [Selection](Selection.html#Selection)]
:::
