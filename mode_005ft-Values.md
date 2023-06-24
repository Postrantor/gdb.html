---
tip: translate by openai@2023-06-24 00:30:14
...
---
description: mode_t Values (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: mode_t Values (Debugging with GDB)
lang: en
resource-type: document
title: mode_t Values (Debugging with GDB)
---
::: header
Next: [Errno Values](Errno-Values.html#Errno-Values)]
:::

---

#### mode_t Values

All values are given in octal representation.

::: smallexample

```bash
  S_IFREG       0100000
  S_IFDIR        040000
  S_IRUSR          0400
  S_IWUSR          0200
  S_IXUSR          0100
  S_IRGRP           040
  S_IWGRP           020
  S_IXGRP           010
  S_IROTH            04
  S_IWOTH            02
  S_IXOTH            01
```

:::
