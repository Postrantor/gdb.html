---
tip: translate by openai@2023-06-23 14:42:42
...
---
description: Traceframe Info Format (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Traceframe Info Format (Debugging with GDB)
lang: en
resource-type: document
title: Traceframe Info Format (Debugging with GDB)
---
::: header
Next: [Branch Trace Format](Branch-Trace-Format.html#Branch-Trace-Format)]
:::

---

### E.18 Traceframe Info Format


To be able to know which objects in the inferior can be examined when inspecting a tracepoint hit, [GDB] needs to obtain the list of memory ranges, registers and trace state variables that have been collected in a traceframe.

> 要知道在检查跟踪点命中时可以检查哪些低级对象，[GDB]需要获取在跟踪帧中收集的内存范围、寄存器和跟踪状态变量的列表。


This list is obtained using the '`qXfer:traceframe-info:read`' (see [qXfer traceframe info read](General-Query-Packets.html#qXfer-traceframe-info-read)) packet and is an XML document.

> 这个列表是使用 'qXfer:traceframe-info:read' (参见[qXfer traceframe info read] (General-Query-Packets.html#qXfer-traceframe-info-read)) 包获得的，是一个XML文档。


[GDB] must be linked with the Expat library to support XML traceframe info discovery. See [Expat](Requirements.html#Expat).

> GDB必须与Expat库链接，以支持XML跟踪帧信息发现。参见[Expat](Requirements.html#Expat)。


The top-level structure of the document is shown below:

> 以下是文档的顶层结构：

::: smallexample

```bash
<?xml version="1.0"?>
<!DOCTYPE traceframe-info
          PUBLIC "+//IDN gnu.org//DTD GDB Memory Map V1.0//EN"
                 "http://sourceware.org/gdb/gdb-traceframe-info.dtd">
<traceframe-info>
   block...
</traceframe-info>
```

:::


Each traceframe block can be either:

> 每个跟踪框架块可以是：

- A region of collected memory starting at `addr` bytes from there:

  ::: smallexample

  ```bash
  <memory start="addr" length="length"/>
  ```

  :::
- A block indicating trace state variable numbered `number` has been collected:

  ::: smallexample

  ```bash
  <tvar id="number"/>
  ```

  :::


The formal DTD for the traceframe info format is given below:

> 以下是跟踪框架信息格式的正式DTD：

::: smallexample

```bash
<!ELEMENT traceframe-info  (memory | tvar)* >
<!ATTLIST traceframe-info  version CDATA   #FIXED  "1.0">

<!ELEMENT memory        EMPTY>
<!ATTLIST memory        start   CDATA   #REQUIRED
                        length  CDATA   #REQUIRED>
<!ELEMENT tvar>
<!ATTLIST tvar          id      CDATA   #REQUIRED>
```

:::
