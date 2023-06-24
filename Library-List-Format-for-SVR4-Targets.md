---
tip: translate by openai@2023-06-23 23:49:08
...
---
description: Library List Format for SVR4 Targets (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Library List Format for SVR4 Targets (Debugging with GDB)
lang: en
resource-type: document
title: Library List Format for SVR4 Targets (Debugging with GDB)
---
::: header
Next: [Memory Map Format](Memory-Map-Format.html#Memory-Map-Format)]
:::

---

### E.15 Library List Format for SVR4 Targets

On SVR4 platforms [GDB] remote protocol.


The '`qXfer:libraries-svr4:read`' packet returns an XML document which lists loaded libraries and their SVR4 linker parameters. For each library on SVR4 target, the following parameters are reported:

> 'qXfer:libraries-svr4:read'数据包会返回一个XML文档，其中列出已加载的库及其SVR4链接器参数。 对于SVR4目标上的每个库，报告以下参数：

- \- `name`, the absolute file name from the `l_name` field of `struct link_map`.
- \- `lm` with address of `struct link_map` used for TLS (Thread Local Storage) access.

- \- `l_addr`, the displacement as read from the field `l_addr` of `struct link_map`. For prelinked libraries this is not an absolute memory address. It is a displacement of absolute memory address against address the file was prelinked to during the library load.

> 从结构体link_map的字段l_addr读取的位移。对于预链接库，这不是绝对内存地址。它是加载库时绝对内存地址与文件预链接地址之间的位移。
- \- `l_ld`, which is memory address of the `PT_DYNAMIC` segment

- \- `lmid`, which is an identifier for a linker namespace, such as the memory address of the `r_debug` object that contains this namespace's load map or the namespace identifier returned by `dlinfo (3)`.

> `- \- `lmid`，这是一个链接器命名空间的标识符，例如包含此命名空间的加载映射的`r_debug`对象的内存地址或者由`dlinfo (3)`返回的命名空间标识符。


Additionally the single `main-lm` attribute specifies address of `struct link_map` used for the main executable. This parameter is used for TLS access and its presence is optional.

> 此外，单个`main-lm`属性指定用于主可执行文件的`struct link_map`的地址。此参数用于TLS访问，其存在是可选的。


[GDB] must be linked with the Expat library to support XML SVR4 library lists. See [Expat](Requirements.html#Expat).

> GDB必须与Expat库链接，以支持XML SVR4库列表。请参见[Expat](Requirements.html#Expat)。


A simple memory map, with two loaded libraries (which do not use prelink), looks like this:

> 一个简单的内存映射，加载了两个不使用预链接的库，看起来像这样：

::: smallexample

```bash
<library-list-svr4 version="1.0" main-lm="0xe4f8f8">
  <library name="/lib/ld-linux.so.2" lm="0xe4f51c" l_addr="0xe2d000"
           l_ld="0xe4eefc" lmid="0xfffe0"/>
  <library name="/lib/libc.so.6" lm="0xe4fbe8" l_addr="0x154000"
           l_ld="0x152350" lmid="0xfffe0"/>
</library-list-svr>
```

:::

The format of an SVR4 library list is described by this DTD:

::: smallexample

```bash
<!-- library-list-svr4: Root element with versioning -->
<!ELEMENT library-list-svr4  (library)*>
<!ATTLIST library-list-svr4  version CDATA   #FIXED  "1.0">
<!ATTLIST library-list-svr4  main-lm CDATA   #IMPLIED>
<!ELEMENT library            EMPTY>
<!ATTLIST library            name    CDATA   #REQUIRED>
<!ATTLIST library            lm      CDATA   #REQUIRED>
<!ATTLIST library            l_addr  CDATA   #REQUIRED>
<!ATTLIST library            l_ld    CDATA   #REQUIRED>
<!ATTLIST library            lmid    CDATA   #IMPLIED>
```

:::

---

::: header
Next: [Memory Map Format](Memory-Map-Format.html#Memory-Map-Format)]
:::
