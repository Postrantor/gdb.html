---
tip: translate by openai@2023-06-24 00:13:03
...
---
description: Memory Map Format (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Memory Map Format (Debugging with GDB)
lang: en
resource-type: document
title: Memory Map Format (Debugging with GDB)
---
::: header
Next: [Thread List Format](Thread-List-Format.html#Thread-List-Format)]
:::

---

### E.16 Memory Map Format


To be able to write into flash memory, [GDB] needs to obtain a memory map from the target. This section describes the format of the memory map.

> 为了能够写入闪存，[GDB]需要从目标获取内存映射。本节描述了内存映射的格式。


The memory map is obtained using the '`qXfer:memory-map:read`' (see [qXfer memory map read](General-Query-Packets.html#qXfer-memory-map-read)) packet and is an XML document that lists memory regions.

> 获取内存映射的方法是使用'qXfer:memory-map:read'（参见[qXfer内存映射读取]（General-Query-Packets.html#qXfer-memory-map-read））数据包，它是一个XML文档，列出了内存区域。


[GDB] must be linked with the Expat library to support XML memory maps. See [Expat](Requirements.html#Expat).

> GDB必须与Expat库链接，以支持XML内存映射。请参阅[Expat](Requirements.html#Expat)。

The top-level structure of the document is shown below:

::: smallexample

```bash
<?xml version="1.0"?>
<!DOCTYPE memory-map
          PUBLIC "+//IDN gnu.org//DTD GDB Memory Map V1.0//EN"
                 "http://sourceware.org/gdb/gdb-memory-map.dtd">
<memory-map>
    region...
</memory-map>
```

:::

Each region can be either:

- A region of RAM starting at `addr` bytes from there:

  ::: smallexample

  ```bash
  <memory type="ram" start="addr" length="length"/>
  ```

  :::
- A region of read-only memory:

  ::: smallexample

  ```bash
  <memory type="rom" start="addr" length="length"/>
  ```

  :::
- A region of flash memory, with erasure blocks `blocksize` bytes in length:

  ::: smallexample

  ```bash
  <memory type="flash" start="addr" length="length">
    <property name="blocksize">blocksize</property>
  </memory>
  ```

  :::


Regions must not overlap. [GDB]' packets to write to addresses in such ranges.

> 区域不得重叠。[GDB] 包必须写入这些范围内的地址。

The formal DTD for memory map format is given below:

::: smallexample

```bash
<!-- ................................................... -->
<!-- Memory Map XML DTD ................................ -->
<!-- File: memory-map.dtd .............................. -->
<!-- .................................... .............. -->
<!-- memory-map.dtd -->
<!-- memory-map: Root element with versioning -->
<!ELEMENT memory-map (memory)*>
<!ATTLIST memory-map    version CDATA   #FIXED  "1.0.0">
<!ELEMENT memory (property)*>
<!-- memory: Specifies a memory region,
             and its type, or device. -->
<!ATTLIST memory        type    (ram|rom|flash) #REQUIRED
                        start   CDATA   #REQUIRED
                        length  CDATA   #REQUIRED>
<!-- property: Generic attribute tag -->
<!ELEMENT property (#PCDATA | property)*>
<!ATTLIST property      name    (blocksize) #REQUIRED>
```

:::

---

::: header
Next: [Thread List Format](Thread-List-Format.html#Thread-List-Format)]
:::
