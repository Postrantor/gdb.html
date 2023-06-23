---
description: Pointer Values (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Pointer Values (Debugging with GDB)
lang: en
resource-type: document
title: Pointer Values (Debugging with GDB)
---
::: header
Next: [Memory Transfer](Memory-Transfer.html#Memory-Transfer)]
:::

---

#### Pointer Values

Pointers to target data are transmitted as they are. An exception is made for pointers to buffers for which the length isn't transmitted as part of the function call, namely strings. Strings are transmitted as a pointer/length pair, both as hex values, e.g.

::: smallexample

```bash
1aaf/12
```

:::

which is a pointer to data of length 18 bytes at position 0x1aaf. The length is defined as the full string length in bytes, including the trailing null byte. For example, the string `"hello world"` at address 0x123456 is transmitted as

::: smallexample

```bash
123456/d
```

:::
