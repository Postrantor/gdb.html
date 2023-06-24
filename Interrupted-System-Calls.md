---
tip: translate by openai@2023-06-23 23:33:46
...
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

> 使用GDB来实现断点和其他停止执行的事件时，会有不幸的副作用。


To handle this problem, your program should check the return value of each system call and react appropriately. This is good programming style anyways.

> 要处理这个问题，你的程序应该检查每个系统调用的返回值，并做出适当的反应。这本身就是一种良好的编程风格。

For example, do not write code like this:

::: smallexample

```bash
  sleep (10);
```

:::


The call to `sleep` will return early if a different thread stops at a breakpoint or for some other reason.

> 调用`sleep`会提前返回，如果另一个线程在断点处停止或由于其他原因。

Instead, write this:

::: smallexample

```bash
  int unslept = 10;
  while (unslept > 0)
    unslept = sleep (unslept);
```

:::


A system call is allowed to return early, so the system is still conforming to its specification. But [GDB].

> 系统调用可以提前返回，因此系统仍然符合其规范。但是[GDB]。


Also, [GDB] uses internal breakpoints in the thread library to monitor certain events such as thread creation and thread destruction. When such an event happens, a system call in another thread may return prematurely, even though your program does not appear to stop.

> 此外，[GDB]在线程库中使用内部断点来监视诸如线程创建和线程销毁等特定事件。当这种事件发生时，另一个线程中的系统调用可能会提前返回，即使您的程序看起来没有停止。
