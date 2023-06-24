---
tip: translate by openai@2023-06-23 20:57:02
...
---
description: Examples (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Examples (Debugging with GDB)
lang: en
resource-type: document
title: Examples (Debugging with GDB)
---
::: header
Next: [File-I/O Remote Protocol Extension](File_002dI_002fO-Remote-Protocol-Extension.html#File_002dI_002fO-Remote-Protocol-Extension)]
:::

---

### E.12 Examples


Example sequence of a target being re-started. Notice how the restart does not get any direct output:

> 示例重新启动目标的序列。注意重新启动没有任何直接输出。

::: smallexample

```bash
-> R00
<- +
target restarts
-> ?
<- +
<- T001:1234123412341234
-> +
```

:::

Example sequence of a target being stepped by a single instruction:

::: smallexample

```bash
-> G1445…
<- +
-> s
<- +
time passes
<- T001:1234123412341234
-> +
-> g
<- +
<- 1455…
-> +
```

:::
