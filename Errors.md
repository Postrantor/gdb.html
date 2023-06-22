---
description: Errors (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Errors (Debugging with GDB)
lang: en
resource-type: document
title: Errors (Debugging with GDB)
---
::: header
Next: [Invalidation](Invalidation.html#Invalidation)]
:::

---

### 28.4 Errors

::: smallexample

```bash
^Z^Zquit
```

:::

This annotation occurs right before [GDB] responds to an interrupt.

::: smallexample

```bash
^Z^Zerror
```

:::

This annotation occurs right before [GDB] responds to an error.

Quit and error annotations indicate that any annotations which [GDB] is immediately returning all the way to the top level.

A quit or error annotation may be preceded by

::: smallexample

```bash
^Z^Zerror-begin
```

:::

Any output between that and the quit or error annotation is the error message.

Warning messages are not yet annotated.
