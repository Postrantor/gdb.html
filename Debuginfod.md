---
tip: translate by openai@2023-06-23 20:27:47
...
---
description: Debuginfod (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Debuginfod (Debugging with GDB)
lang: en
resource-type: document
title: Debuginfod (Debugging with GDB)
---
::: header
Next: [Man Pages](Man-Pages.html#Man-Pages)]
:::

---

## Appendix K Download debugging resources with Debuginfod

`debuginfod` is an HTTP server for distributing ELF, DWARF and source files.


With the `debuginfod` client library, `libdebuginfod` can query servers using the build IDs associated with missing debug info, executables and source files in order to download them on demand.

> 使用`debuginfod`客户端库`libdebuginfod`，可以查询服务器，使用与缺失调试信息、可执行文件和源文件相关联的构建ID，以便按需下载它们。


For instructions on building [GDB], see [--with-debuginfod](Configure-Options.html#Configure-Options). `debuginfod` is packaged with `elfutils`, starting with version 0.178. See [https://sourceware.org/elfutils/Debuginfod.html](https://sourceware.org/elfutils/Debuginfod.html) for more information regarding `debuginfod`.

> 对于如何构建GDB的指示，请参阅--with-debuginfod（Configure-Options.html#Configure-Options）。从0.178版本开始，debuginfod将与elfutils一起打包。有关debuginfod的更多信息，请参阅https://sourceware.org/elfutils/Debuginfod.html。

---

• [Debuginfod Settings](Debuginfod-Settings.html#Debuginfod-Settings)

---
