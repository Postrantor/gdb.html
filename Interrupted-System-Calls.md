---
description: Interrupted System Calls (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Interrupted System Calls (Debugging with GDB)
lang: en
resource-type: document
title: Interrupted System Calls (Debugging with GDB)
---
::: header
Next: [Observer Mode](Observer-Mode.html#Observer-Mode)]
:::

---

#### 5.5.5 Interrupted System Calls

There is an unfortunate side effect when using [GDB] uses to implement breakpoints and other events that stop execution.

To handle this problem, your program should check the return value of each system call and react appropriately. This is good programming style anyways.

For example, do not write code like this:

::: smallexample

```bash
  sleep (10);
```

:::

The call to `sleep` will return early if a different thread stops at a breakpoint or for some other reason.

Instead, write this:

::: smallexample

```bash
  int unslept = 10;
  while (unslept > 0)
    unslept = sleep (unslept);
```

:::

A system call is allowed to return early, so the system is still conforming to its specification. But [GDB].

Also, [GDB] uses internal breakpoints in the thread library to monitor certain events such as thread creation and thread destruction. When such an event happens, a system call in another thread may return prematurely, even though your program does not appear to stop.
