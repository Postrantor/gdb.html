---
tip: translate by openai@2023-06-24 01:05:43
...
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

> 指向目标数据的指针会原样传输。但是指向缓冲区的指针除外，这些指针的长度不会随着函数调用一起传输，也就是字符串。字符串会作为指针/长度对，以十六进制值的形式传输。

::: smallexample

```bash
1aaf/12
```

:::


which is a pointer to data of length 18 bytes at position 0x1aaf. The length is defined as the full string length in bytes, including the trailing null byte. For example, the string `"hello world"` at address 0x123456 is transmitted as

> 指向位置0x1aaf处的18字节数据的指针。长度指的是包括尾部空字节在内的完整字符串的字节数。例如，位置0x123456处的字符串“hello world”被传输为

::: smallexample

```bash
123456/d
```

:::
