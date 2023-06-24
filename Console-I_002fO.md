---
tip: translate by openai@2023-06-23 19:36:18
...
---
description: Console I/O (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Console I/O (Debugging with GDB)
lang: en
resource-type: document
title: Console I/O (Debugging with GDB)
---
::: header
Next: [List of Supported Calls](List-of-Supported-Calls.html#List-of-Supported-Calls)]
:::

---

#### E.13.6 Console I/O


By default and if not explicitly closed by the target system, the file descriptors 0, 1 and 2 are connected to the [GDB] so that after the target read request from file descriptor 0 all following typing is buffered until either one of the following conditions is met:

> 默认情况下，如果目标系统没有明确关闭，文件描述符0、1和2将连接到[GDB]，这样，在目标从文件描述符0读取请求之后，所有随后的输入都将被缓冲，直到满足以下任一条件：


- The user types [Ctrl-c]. The behaviour is as explained above, and the `read` system call is treated as finished.

> 用户输入[Ctrl-c]。行为如上所述，`read`系统调用被视为完成。
- The user presses RET. This is treated as end of input with a trailing newline.
- The user types [Ctrl-d]') is appended to the input.


If the user has typed more characters than fit in the buffer given to the `read` call, the trailing characters are buffered in [GDB] until either another `read(0, …)` is requested by the target, or debugging is stopped at the user's request.

> 如果用户输入的字符数超过了给定给`read`调用的缓冲区容量，那么尾随字符将会被缓冲到[GDB]中，直到目标另外请求`read(0, ...)`，或者用户要求停止调试。
