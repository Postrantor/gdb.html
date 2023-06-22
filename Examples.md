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
