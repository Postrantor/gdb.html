---
tip: translate by openai@2023-06-23 18:09:03
...
---
description: Branch Trace Format (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Branch Trace Format (Debugging with GDB)
lang: en
resource-type: document
title: Branch Trace Format (Debugging with GDB)
---
::: header
Next: [Branch Trace Configuration Format](Branch-Trace-Configuration-Format.html#Branch-Trace-Configuration-Format)]
:::

---

### E.19 Branch Trace Format


In order to display the branch trace of an inferior thread, [GDB] needs to obtain the list of branches. This list is represented as list of sequential code blocks that are connected via branches. The code in each block has been executed sequentially.

> 为了显示次级线程的分支跟踪，[GDB]需要获取分支列表。该列表表示为通过分支连接的顺序代码块列表。每个块中的代码已经按顺序执行。


This list is obtained using the '`qXfer:btrace:read`' (see [qXfer btrace read](General-Query-Packets.html#qXfer-btrace-read)) packet and is an XML document.

> 这个列表是使用'qXfer:btrace:read'（参见[qXfer btrace read]（General-Query-Packets.html#qXfer-btrace-read））数据包获得的，是一个XML文档。


[GDB] must be linked with the Expat library to support XML traceframe info discovery. See [Expat](Requirements.html#Expat).

> GDB必须与Expat库链接，以支持XML跟踪框架信息发现。请参见[Expat](Requirements.html#Expat)。


The top-level structure of the document is shown below:

> 以下是文档的顶级结构：

::: smallexample

```bash
<?xml version="1.0"?>
<!DOCTYPE btrace
          PUBLIC "+//IDN gnu.org//DTD GDB Branch Trace V1.0//EN"
                 "http://sourceware.org/gdb/gdb-btrace.dtd">
<btrace>
   block...
</btrace>
```

:::

- A block of sequentially executed instructions starting at `begin`:

  ::: smallexample

  ```bash
  <block begin="begin" end="end"/>
  ```

  :::


The formal DTD for the branch trace format is given below:

> 以下是分支跟踪格式的正式DTD：

::: smallexample

```bash
<!ELEMENT btrace  (block* | pt) >
<!ATTLIST btrace  version CDATA   #FIXED "1.0">

<!ELEMENT block        EMPTY>
<!ATTLIST block        begin  CDATA   #REQUIRED
                       end    CDATA   #REQUIRED>

<!ELEMENT pt (pt-config?, raw?)>

<!ELEMENT pt-config (cpu?)>

<!ELEMENT cpu EMPTY>
<!ATTLIST cpu vendor   CDATA #REQUIRED
              family   CDATA #REQUIRED
              model    CDATA #REQUIRED
              stepping CDATA #REQUIRED>

<!ELEMENT raw (#PCDATA)>
```

:::
