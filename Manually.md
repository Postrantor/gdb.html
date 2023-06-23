---
description: Manually (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Manually (Debugging with GDB)
lang: en
resource-type: document
title: Manually (Debugging with GDB)
---
::: header
Next: [Automatically](Automatically.html#Automatically)]
:::

---

#### 15.1.2 Setting the Working Language

If you allow [GDB] to set the language automatically, expressions are interpreted the same way in your debugging session and your program.

If you wish, you may set the language manually. To do this, issue the command '`set language lang`'.

Setting the language manually prevents [GDB] was parsing Modula-2, a command such as:

::: smallexample

```bash
print a = b + c
```

:::

might not have the effect you intended. In C, this means to add `b` and `c` and place the result in `a`. The result printed would be the value of `a`. In Modula-2, this means to compare `a` to the result of `b+c`, yielding a `BOOLEAN` value.
