---
tip: translate by openai@2023-06-23 17:16:32
...
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

> 当程序由像`步进`或`继续`这样的GDB命令开始执行时

::: smallexample

```bash
^Z^Zstarting
```

:::


is output. When the program stops,

> 当程序停止时，是输出。

::: smallexample

```bash
^Z^Zstopped
```

:::


is output. Before the `stopped` annotation, a variety of annotations describe how the program stopped.

> 在`停止`注释之前，各种注释描述了程序是如何停止的。

`^Z^Zexited exit-status`


The program exited, and `exit-status` is the exit status (zero for successful exit, otherwise nonzero).

> 程序已退出，`exit-status` 是退出状态（成功退出时为零，否则为非零值）。

`^Z^Zsignalled`


The program exited with a signal. After the `^Z^Zsignalled`, the annotation continues:

> 程序以信号退出。在“^Z^Z发出信号”之后，注释继续：转换为简体中文。

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

> 在哪里，`名称`是为了用户的利益而设置的，没有特定的格式。

`^Z^Zsignal`


The syntax of this annotation is just like `signalled`, but [GDB] is just saying that the program received the signal, not that it was terminated with it.

> 这个注释的语法就像 'signalled' 一样，但是GDB只是表示程序收到了信号，而不是它被信号终止了。

`^Z^Zbreakpoint number`


The program hit breakpoint number `number`.

> 程序遇到断点号码`number`。

`^Z^Zwatchpoint number`


The program hit watchpoint number `number`.

> 程序触及断点编号`number`。
