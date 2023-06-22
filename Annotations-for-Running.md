---
description: Annotations for Running (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Annotations for Running (Debugging with GDB)
lang: en
resource-type: document
title: Annotations for Running (Debugging with GDB)
---
::: header
Next: [Source Annotations](Source-Annotations.html#Source-Annotations)]
:::

---

### 28.6 Running the Program

When the program starts executing due to a [GDB] command such as `step` or `continue`,

::: smallexample

```bash
^Z^Zstarting
```

:::

is output. When the program stops,

::: smallexample

```bash
^Z^Zstopped
```

:::

is output. Before the `stopped` annotation, a variety of annotations describe how the program stopped.

`^Z^Zexited exit-status`

The program exited, and `exit-status` is the exit status (zero for successful exit, otherwise nonzero).

`^Z^Zsignalled`

The program exited with a signal. After the `^Z^Zsignalled`, the annotation continues:

::: smallexample

```bash
intro-text
^Z^Zsignal-name
name
^Z^Zsignal-name-end
middle-text
^Z^Zsignal-string
string
^Z^Zsignal-string-end
end-text
```

:::

where `name` are for the user's benefit and have no particular format.

`^Z^Zsignal`

The syntax of this annotation is just like `signalled`, but [GDB] is just saying that the program received the signal, not that it was terminated with it.

`^Z^Zbreakpoint number`

The program hit breakpoint number `number`.

`^Z^Zwatchpoint number`

The program hit watchpoint number `number`.
