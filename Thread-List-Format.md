---
tip: translate by openai@2023-06-23 14:29:07
...
---
description: Thread List Format (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Thread List Format (Debugging with GDB)
lang: en
resource-type: document
title: Thread List Format (Debugging with GDB)
----------------------------------------------

::: header
Next: [Traceframe Info Format](Traceframe-Info-Format.html#Traceframe-Info-Format)]
:::

---

### E.17 Thread List Format

To efficiently update the list of threads and their attributes, [GDB]' packet (see [qXfer threads read](General-Query-Packets.html#qXfer-threads-read)) and obtains the XML document with the following structure:

> 为了有效地更新线程列表及其属性，[GDB]包（参见[qXfer threads read]（General-Query-Packets.html#qXfer-threads-read））获取具有以下结构的 XML 文档：

::: smallexample

```bash
<?xml version="1.0"?>
<threads>
    <thread id="id" core="0" name="name">
    ... description ...
    </thread>
</threads>
```

:::

Each '`thread`' attribute, if present, is a hex encoded representation of the thread handle.

> 每个 `thread` 属性（如果存在）是线程句柄的十六进制编码表示。
