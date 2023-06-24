---
tip: translate by openai@2023-06-24 00:31:31
...
---
description: Multiple Extension Languages (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Multiple Extension Languages (Debugging with GDB)
lang: en
resource-type: document
title: Multiple Extension Languages (Debugging with GDB)
---
::: header
Previous: [Auto-loading extensions](Auto_002dloading-extensions.html#Auto_002dloading-extensions)]
:::

---

### 23.6 Multiple Extension Languages


The Guile and Python extension languages do not share any state, and generally do not interfere with each other. There are some things to be aware of, however.

> Python和Guile扩展语言不共享任何状态，一般不会相互干扰。但是，还是需要注意一些事情。

#### 23.6.1 Python comes first


Python was [GDB] maintains a list of enabled extension languages, and when it makes a call to an extension language, (say to pretty-print a value), it tries each in turn until an extension language indicates it has performed the request (e.g., has returned the pretty-printed form of a value). This extends to errors while performing such requests: If an error happens while, for example, trying to pretty-print an object then the error is reported and any following extension languages are not tried.

> Python会维护一个已启用的扩展语言列表，当它调用扩展语言时（比如用于美化值），它会依次尝试每个扩展语言，直到有一个扩展语言表明它已经完成了请求（比如已经返回了美化后的值）。这也适用于在执行这样的请求时发生的错误：如果在尝试美化对象时发生错误，那么就会报告错误，并且不会尝试后续的扩展语言。
