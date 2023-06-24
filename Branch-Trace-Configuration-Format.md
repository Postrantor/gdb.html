---
tip: translate by openai@2023-06-23 18:08:32
...
---
description: Branch Trace Configuration Format (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Branch Trace Configuration Format (Debugging with GDB)
lang: en
resource-type: document
title: Branch Trace Configuration Format (Debugging with GDB)
---
::: header
Previous: [Branch Trace Format](Branch-Trace-Format.html#Branch-Trace-Format)]
:::

---

### E.20 Branch Trace Configuration Format


For each inferior thread, [GDB]' (see [qXfer btrace-conf read](General-Query-Packets.html#qXfer-btrace_002dconf-read)) packet.

> 对于每个次级线程，[GDB]（参见[qXfer btrace-conf read]（General-Query-Packets.html#qXfer-btrace_002dconf-read））数据包。


The configuration describes the branch trace format and configuration settings for that format. The following information is described:

> 配置描述了分支跟踪格式以及该格式的配置设置。下面的信息被描述：

`bts`


:   This thread uses the *Branch Trace Store* (BTS) format.

> 这个线程使用*分支跟踪存储*（BTS）格式。

```
`size`

:   The size of the BTS ring buffer in bytes.
```

`pt`


:   This thread uses the *Intel Processor Trace* (Intel PT) format.

> 这个线程使用*Intel处理器跟踪（Intel PT）格式。

```
`size`

:   The size of the Intel PT ring buffer in bytes.
```


[GDB] must be linked with the Expat library to support XML branch trace configuration discovery. See [Expat](Requirements.html#Expat).

> GDB必须与Expat库链接，以支持XML分支跟踪配置发现。请参见[Expat](Requirements.html#Expat)。


The formal DTD for the branch trace configuration format is given below:

> 以下给出了分支跟踪配置格式的正式DTD：

::: smallexample

```bash
<!ELEMENT btrace-conf  (bts?, pt?)>
<!ATTLIST btrace-conf    version CDATA   #FIXED "1.0">

<!ELEMENT bts    EMPTY>
<!ATTLIST bts    size    CDATA   #IMPLIED>

<!ELEMENT pt EMPTY>
<!ATTLIST pt size    CDATA   #IMPLIED>
```

:::
