---
description: Backtrace (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Backtrace (Debugging with GDB)
lang: en
resource-type: document
title: Backtrace (Debugging with GDB)
---
::: header
Next: [Selection](Selection.html#Selection)]
:::

---

### 8.2 Backtraces

A backtrace is a summary of how your program got where it is. It shows one line per frame, for many frames, starting with the currently executing frame (frame zero), followed by its caller (frame one), and on up the stack.

To print a backtrace of the entire stack, use the `backtrace` command, or its alias `bt`. This command will print one line per frame for frames in the stack. By default, all stack frames are printed. You can stop the backtrace at any time by typing the system interrupt character, normally [Ctrl-c].

`backtrace [option]… [qualifier]… [count]`
`bt [option]… [qualifier]… [count]`

:   Print the backtrace of the entire stack.

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

In a multi-threaded program, [GDB] will display the backtrace for all the threads; this is handy when you debug a core dump of a multi-threaded program.

Each line in the backtrace shows the frame number and the function name. The program counter value is also shown---unless you use `set print address off`. The backtrace also shows the source file name and line number, as well as the arguments to the function. The program counter value is omitted if it is at the beginning of the code for that line number.

Here is an example of a backtrace. It was made with the command '`bt 3`', so it shows the innermost three frames.

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

The value of parameter `data` in frame 1 has been replaced by `…`. By default, [GDB] (see [Print Settings](Print-Settings.html#Print-Settings)) controls what frame information is printed.

If your program was compiled with optimizations, some compilers will optimize away arguments passed to functions if those arguments are never used after the call. Such optimizations generate code that passes arguments through registers, but doesn't store those arguments in the stack frame. [GDB] has no way of displaying such arguments in stack frames other than the innermost one. Here's what such a backtrace might look like:

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

If you need to display the values of such optimized-out arguments, either deduce that from other variables whose values depend on the one you are interested in, or recompile without optimizations.

Most programs have a standard user entry point---a place where system libraries and startup code transition into user code. For C this is `main`[^9^](#FOOT9) finds the entry function in a backtrace it will terminate the backtrace, to avoid tracing into highly system-specific (and generally uninteresting) code.

If you need to examine the startup code, or limit the number of levels in a backtrace, you can change this behavior:

`set backtrace past-main`
`set backtrace past-main on`

:

```
Backtraces will continue past the user entry point.
```

`set backtrace past-main off`

:   Backtraces will stop when they encounter the user entry point. This is the default.

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

`show backtrace past-entry`

:   Display the current internal entry point backtrace policy.

`set backtrace limit n`
`set backtrace limit 0`
`set backtrace limit unlimited`

:

```
Limit the backtrace to `n` levels. A value of `unlimited` or zero means unlimited levels.
```

`show backtrace limit`

:   Display the current limit on backtrace levels.

You can control how file names are displayed.

`set filename-display`
`set filename-display relative`

:

```
Display file names relative to the compilation directory. This is the default.
```

`set filename-display basename`

:   Display only basename of a filename.

`set filename-display absolute`

:   Display an absolute filename.

`show filename-display`

:   Show the current way to display filenames.

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
