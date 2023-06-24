---
tip: translate by openai@2023-06-23 23:49:52
...
---
description: Library List Format (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Library List Format (Debugging with GDB)
lang: en
resource-type: document
title: Library List Format (Debugging with GDB)
---
::: header
Next: [Library List Format for SVR4 Targets](Library-List-Format-for-SVR4-Targets.html#Library-List-Format-for-SVR4-Targets)]
:::

---

### E.14 Library List Format


On some platforms, a dynamic loader (e.g. `ld.so`' packet (see [qXfer library list read](General-Query-Packets.html#qXfer-library-list-read)) instead. The remote stub queries the target's operating system and reports which libraries are loaded.

> 在某些平台上，动态加载器（例如`ld.so`）包（参见[qXfer library list read]（General-Query-Packets.html#qXfer-library-list-read））可用于代替。远程存根查询目标操作系统，并报告哪些库被加载。


The '`qXfer:libraries:read`' packet returns an XML document which lists loaded libraries and their offsets. Each library has an associated name and one or more segment or section base addresses, which report where the library was loaded in memory.

> 'qXfer:libraries:read'数据包会返回一个XML文档，其中列出了加载的库及其偏移量。每个库都有一个关联的名称，以及一个或多个段或节基地址，报告了库在内存中的加载位置。


For the common case of libraries that are fully linked binaries, the library should have a list of segments. If the target supports dynamic linking of a relocatable object file, its library XML element should instead include a list of allocated sections. The segment or section bases are start addresses, not relocation offsets; they do not depend on the library's link-time base addresses.

> 对于完全链接的库的普遍情况，该库应具有一个段列表。如果目标支持可重定位对象文件的动态链接，它的库XML元素应该包含一个分配段的列表。段或节的基地是起始地址，而不是重定位偏移量；它们不依赖于库的链接时基地址。


[GDB] must be linked with the Expat library to support XML library lists. See [Expat](Requirements.html#Expat).

> GDB必须链接到Expat库以支持XML库列表。请参见[Expat](Requirements.html#Expat)。


A simple memory map, with one loaded library relocated by a single offset, looks like this:

> 一个简单的内存映射，通过单个偏移量重定位了一个已加载的库，看起来像这样：

::: smallexample

```bash
<library-list>
  <library name="/lib/libc.so.6">
    <segment address="0x10000000"/>
  </library>
</library-list>
```

:::


Another simple memory map, with one loaded library with three allocated sections (.text, .data, .bss), looks like this:

> 另一个简单的内存映射，加载了一个带有三个分配区域（.text，.data，.bss）的库，看起来像这样：

::: smallexample

```bash
<library-list>
  <library name="sharedlib.o">
    <section address="0x10000000"/>
    <section address="0x20000000"/>
    <section address="0x30000000"/>
  </library>
</library-list>
```

:::

The format of a library list is described by this DTD:

::: smallexample

```bash
<!-- library-list: Root element with versioning -->
<!ELEMENT library-list  (library)*>
<!ATTLIST library-list  version CDATA   #FIXED  "1.0">
<!ELEMENT library       (segment*, section*)>
<!ATTLIST library       name    CDATA   #REQUIRED>
<!ELEMENT segment       EMPTY>
<!ATTLIST segment       address CDATA   #REQUIRED>
<!ELEMENT section       EMPTY>
<!ATTLIST section       address CDATA   #REQUIRED>
```

:::


In addition, segments and section descriptors cannot be mixed within a single library element, and you must supply at least one segment or section for each library.

> 此外，在单个库元素中不能混合使用段和节描述符，您必须为每个库提供至少一个段或节。

---

::: header
Next: [Library List Format for SVR4 Targets](Library-List-Format-for-SVR4-Targets.html#Library-List-Format-for-SVR4-Targets)]
:::
