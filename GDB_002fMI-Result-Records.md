---
tip: translate by openai@2023-06-23 22:08:59
...
---
description: GDB/MI Result Records (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: GDB/MI Result Records (Debugging with GDB)
lang: en
resource-type: document
title: GDB/MI Result Records (Debugging with GDB)
---
::: header
Next: [GDB/MI Stream Records](GDB_002fMI-Stream-Records.html#GDB_002fMI-Stream-Records)]
:::

---

#### 27.5.1 [GDB/MI]


In addition to a number of out-of-band notifications, the response to a [GDB/MI] command includes one of the following result indications:

> 此外，[GDB/MI]命令的响应还包括以下结果指示之一：

`"^done" [ "," results ]`


The synchronous operation was successful, `results` are the return values.

> 同步操作成功，`结果`是返回值。

`"^running"`


This result record is equivalent to '`^done`' output record to determine which threads are resumed.

> 这个结果记录等价于'^done'输出记录，以确定哪些线程被恢复。

`"^connected"`

[GDB] has connected to a remote target.

`"^error" "," "msg=" c-string [ "," "code=" c-string ]`


The operation failed. The `msg=c-string` variable contains the corresponding error message.

> 操作失败。变量`msg=c-string`包含相应的错误消息。


If present, the `code=c-string` variable provides an error code on which consumers can rely on to detect the corresponding error condition. At present, only one error code is defined:

> 如果存在，`code=c-string`变量提供了一个错误代码，消费者可以依靠它来检测相应的错误条件。目前只定义了一个错误代码。

'`"undefined-command"`'

:   Indicates that the command causing the error does not exist.

`"^exit"`

[GDB] has terminated.
