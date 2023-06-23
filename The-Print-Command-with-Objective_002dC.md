---
description: The Print Command with Objective-C (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: The Print Command with Objective-C (Debugging with GDB)
lang: en
resource-type: document
title: The Print Command with Objective-C (Debugging with GDB)
---
::: header
Previous: [Method Names in Commands](Method-Names-in-Commands.html#Method-Names-in-Commands)]
:::

---

#### 15.4.4.2 The Print Command With Objective-C

The print command has also been extended to accept methods. For example:

::: smallexample

```bash
print -[object hash]
```

:::

will tell [GDB] and print the result. Also, an additional command has been added, `print-object` or `po` for short, which is meant to print the description of an object. However, this command may only work with certain Objective-C libraries that have a particular hook function, `_NSPrintForDebugger`, defined.
