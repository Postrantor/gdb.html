---
tip: translate by openai@2023-06-23 15:22:09
...
---
description: Using JIT Debug Info Readers (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Using JIT Debug Info Readers (Debugging with GDB)
lang: en
resource-type: document
title: Using JIT Debug Info Readers (Debugging with GDB)
--------------------------------------------------------

::: header
Next: [Writing JIT Debug Info Readers](Writing-JIT-Debug-Info-Readers.html#Writing-JIT-Debug-Info-Readers)]
:::

---

#### 30.4.1 Using JIT Debug Info Readers

Readers can be loaded and unloaded using the `jit-reader-load` and `jit-reader-unload` commands.

> 读者可以使用 `jit-reader-load` 和 `jit-reader-unload` 命令加载和卸载。

`jit-reader-load reader`

:   Load the JIT reader named `reader`).

> 载入名为 `reader` 的 JIT 阅读器。

```
Only one reader can be active at a time; trying to load a second reader when one is already loaded will result in [GDB] reporting an error. A new JIT reader can be loaded by first unloading the current one using `jit-reader-unload` and then invoking `jit-reader-load`.
```

`jit-reader-unload`

:   Unload the currently loaded JIT reader.

> 卸载当前加载的 JIT 阅读器。
