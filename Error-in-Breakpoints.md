---
tip: translate by openai@2023-06-23 20:52:13
...
---
description: Error in Breakpoints (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Error in Breakpoints (Debugging with GDB)
lang: en
resource-type: document
title: Error in Breakpoints (Debugging with GDB)
---
::: header
Next: [Breakpoint-related Warnings](Breakpoint_002drelated-Warnings.html#Breakpoint_002drelated-Warnings)]
:::

---

#### 5.1.11 "Cannot insert breakpoints"


If you request too many active hardware-assisted breakpoints and watchpoints, you will see this error message:

> 如果您请求太多的主动硬件辅助断点和监视点，您将会看到此错误消息：

::: smallexample

```bash
Stopped; cannot insert breakpoints.
You may have requested too many hardware breakpoints and watchpoints.
```

:::


This message is printed when you attempt to resume the program, since only then [GDB] knows exactly how many hardware breakpoints and watchpoints it needs to insert.

> 当你尝试恢复程序时，此消息将被打印，因为只有那时[GDB]才知道需要插入多少硬件断点和监视点。


When this message is printed, you need to disable or remove some of the hardware-assisted breakpoints and watchpoints, and then continue.

> 当此消息打印出来时，您需要禁用或移除一些硬件辅助断点和监视点，然后继续。
