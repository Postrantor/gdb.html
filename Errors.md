---
tip: translate by openai@2023-06-23 20:52:35
...
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

> 退出和错误注释表明，[GDB]立即将所有注释返回到最顶层。

A quit or error annotation may be preceded by

::: smallexample

```bash
^Z^Zerror-begin
```

:::


Any output between that and the quit or error annotation is the error message.

> 任何在该输出和退出或错误注释之间的输出都是错误消息。

Warning messages are not yet annotated.
