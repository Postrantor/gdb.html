---
tip: translate by openai@2023-06-24 00:22:50
...
---
description: MIPS Embedded (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: MIPS Embedded (Debugging with GDB)
lang: en
resource-type: document
title: MIPS Embedded (Debugging with GDB)
---
::: header
Next: [OpenRISC 1000](OpenRISC-1000.html#OpenRISC-1000)]
:::

---

#### 21.3.6 MIPS Embedded

[GDB] supports these special commands for MIPS targets:

`set mipsfpu double`
`set mipsfpu single`
`set mipsfpu none`
`set mipsfpu auto`
`show mipsfpu`

:

```
If your target board does not support the MIPS floating point coprocessor, you should use the command '`set mipsfpu none`'.

In previous versions the only choices were double precision or no floating point, so '`set mipsfpu on`' will select no floating point.

As usual, you can inquire about the `mipsfpu` variable with '`show mipsfpu`'.
```
