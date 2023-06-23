---
description: Selection (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Selection (Debugging with GDB)
lang: en
resource-type: document
title: Selection (Debugging with GDB)
---
::: header
Next: [Frame Info](Frame-Info.html#Frame-Info)]
:::

---

### 8.3 Selecting a Frame

Most commands for examining the stack and other data in your program work on whichever stack frame is selected at the moment. Here are the commands for selecting a stack frame; all of them finish by printing a brief description of the stack frame just selected.

`frame [ frame-selection-spec ]`

`f [ frame-selection-spec ]`

The `frame` command allows different stack frames to be selected. The `frame-selection-spec` can be any of the following:

`num`

`level num`

Select frame level `num`. Recall that frame zero is the innermost (currently executing) frame, frame one is the frame that called the innermost one, and so on. The highest level frame is usually the one for `main`.

As this is the most common method of navigating the frame stack, the string `level` can be omitted. For example, the following two commands are equivalent:

::: smallexample

```bash
(gdb) frame 3
(gdb) frame level 3
```

:::

`address stack-address`

Select the frame with stack address `stack-address` for a frame can be seen in the output of `info frame`, for example:

::: smallexample

```bash
(gdb) info frame
Stack level 1, frame at 0x7fffffffda30:
 rip = 0x40066d in b (amd64-entry-value.cc:59); saved rip 0x4004c5
 tail call frame, caller of frame at 0x7fffffffda30
 source language c++.
 Arglist at unknown address.
 Locals at unknown address, Previous frame's sp is 0x7fffffffda30
```

:::

The `stack-address` for this frame is `0x7fffffffda30` as indicated by the line:

::: smallexample

```bash
Stack level 1, frame at 0x7fffffffda30:
```

:::

`function function-name`

Select the stack frame for function `function-name` then the inner most stack frame is selected.

`view stack-address [ pc-addr ]`

View a frame that is not part of [GDB].

This is useful mainly if the chaining of stack frames has been damaged by a bug, making it impossible for [GDB] to assign numbers properly to all frames. In addition, this can be useful when your program has multiple stacks and switches between them.

When viewing a frame outside the current backtrace using `frame view` then you can always return to the original stack using one of the previous stack frame selection instructions, for example `frame level 0`.

`up n`

Move `n`, this advances toward the outermost frame, to higher frame numbers, to frames that have existed longer.

`down n`

Move `n`, this advances toward the innermost frame, to lower frame numbers, to frames that were created more recently. You may abbreviate `down` as `do`.

All of these commands end by printing two lines of output describing the frame. The first line shows the frame number, the function name, the arguments, and the source file and line number of execution in that frame. The second line shows the text of that source line.

For example:

::: smallexample

```bash
(gdb) up
#1  0x22f0 in main (argc=1, argv=0xf7fffbf4, env=0xf7fffbfc)
    at env.c:10
10              read_input_file (argv[i]);
```

:::

After such a printout, the `list` command with no arguments prints ten lines centered on the point of execution in the frame. You can also edit the program at the point of execution with your favorite editing program by typing `edit`. See [Printing Source Lines](List.html#List), for details.

`select-frame [ frame-selection-spec ]`

The `select-frame` command is a variant of `frame` that does not display the new frame after selecting it. This command is intended primarily for use in [GDB] is as for the `frame` command described in [Selecting a Frame](#Selection).

`up-silently n`

`down-silently n`

These two commands are variants of `up` and `down`, respectively; they differ in that they do their work silently, without causing display of the new frame. They are intended primarily for use in [GDB] command scripts, where the output might be unnecessary and distracting.

---

::: header
Next: [Frame Info](Frame-Info.html#Frame-Info)]
:::
