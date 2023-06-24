---
tip: translate by openai@2023-06-23 18:08:26
...
---
description: BPF (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: BPF (Debugging with GDB)
lang: en
resource-type: document
title: BPF (Debugging with GDB)
---
::: header
Next: [M68K](M68K.html#M68K)]
:::

---

#### 21.3.3 BPF

`target sim [simargs] …`


:   The [GDB] BPF simulator accepts the following optional arguments.

> BPF模拟器可接受以下可选参数。

```
`--skb-data-offset=offset`

:   Tell the simulator the offset, measured in bytes, of the `skb_data` field in the kernel `struct sk_buff` structure. This offset is used by some BPF specific-purpose load/store instructions. Defaults to 0.
```
