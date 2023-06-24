---
tip: translate by openai@2023-06-24 02:10:21
...
---
description: Retrieving Descriptions (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Retrieving Descriptions (Debugging with GDB)
lang: en
resource-type: document
title: Retrieving Descriptions (Debugging with GDB)
---
::: header
Next: [Target Description Format](Target-Description-Format.html#Target-Description-Format)]
:::

---

### G.1 Retrieving Descriptions


Target descriptions can be read from the target automatically, or specified by the user manually. The default behavior is to read the description from the target. [GDB]' annex are an XML document, of the form described in [Target Description Format](Target-Description-Format.html#Target-Description-Format).

> 目标描述可以从目标自动读取，或由用户手动指定。默认行为是从目标读取描述。[GDB]附件是一个XML文档，格式如[目标描述格式](Target-Description-Format.html#Target-Description-Format)所述。


Alternatively, you can specify a file to read for the target description. If a file is set, the target will not be queried. The commands to specify a file are:

> 另外，您还可以指定一个文件来读取目标描述。 如果设置了文件，则不会查询目标。 指定文件的命令是：

`set tdesc filename path`

Read the target description from `path`.

`unset tdesc filename`


Do not read the XML target description from a file. [GDB] will use the description supplied by the current target.

> 不要从文件中读取XML目标描述。[GDB]将使用当前目标提供的描述。

`show tdesc filename`

Show the filename to read for a target description, if any.
