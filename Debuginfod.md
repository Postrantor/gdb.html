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

For instructions on building [GDB], see [--with-debuginfod](Configure-Options.html#Configure-Options). `debuginfod` is packaged with `elfutils`, starting with version 0.178. See [https://sourceware.org/elfutils/Debuginfod.html](https://sourceware.org/elfutils/Debuginfod.html) for more information regarding `debuginfod`.

---

• [Debuginfod Settings](Debuginfod-Settings.html#Debuginfod-Settings)

---
