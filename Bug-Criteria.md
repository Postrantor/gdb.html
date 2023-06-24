---
tip: translate by openai@2023-06-23 18:28:23
...
---
description: Bug Criteria (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Bug Criteria (Debugging with GDB)
lang: en
resource-type: document
title: Bug Criteria (Debugging with GDB)
---
::: header
Next: [Bug Reporting](Bug-Reporting.html#Bug-Reporting)]
:::

---

### 32.1 Have You Found a Bug?


If you are not sure whether you have found a bug, here are some guidelines:

> 如果你不确定你是否发现了一个 bug，这里有一些指导原则：

- bug. Reliable debuggers never crash.

- produces an error message for valid input, that is a bug. (Note that if you're cross debugging, the problem may also be somewhere in the connection to the target.)

> 当输入有效时，出现错误消息就是一个 bug。（注意，如果你正在进行跨调试，问题也可能出现在与目标的连接中。）

- does not produce an error message for invalid input, that is a bug. However, you should note that your idea of "invalid input" might be our idea of "an extension" or "support for traditional practice".

> - 对无效输入不会产生错误消息，这是一个bug。但是，你应该注意，你对“无效输入”的理解可能是我们对“扩展”或“支持传统实践”的理解。

- If you are an experienced user of debugging tools, your suggestions for improvement of [GDB] are welcome in any case.

> 如果你是一位有经验的调试工具用户，不管怎样，你对[GDB]的改进建议都是受欢迎的。
