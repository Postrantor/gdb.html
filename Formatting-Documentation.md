---
tip: translate by openai@2023-06-23 21:15:51
...
---
description: Formatting Documentation (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Formatting Documentation (Debugging with GDB)
lang: en
resource-type: document
title: Formatting Documentation (Debugging with GDB)
---
::: header
Next: [Installing GDB](Installing-GDB.html#Installing-GDB)]
:::

---

## Appendix B Formatting Documentation

The [GDB].


The release also includes the source for the reference card. You can format it, using TeX, by typing:

> 另外，发布也包括参考卡的源代码。您可以使用TeX来格式化它，只需输入：

::: smallexample

```bash
make refcard.dvi
```

:::

The [GDB] output program.


All the documentation for [GDB] comes as part of the machine-readable distribution. The documentation is written in Texinfo format, which is a documentation system that uses a single source file to produce both on-line information and a printed manual. You can use one of the Info formatting commands to create the on-line version of the documentation and TeX (or `texi2roff`) to typeset the printed version.

> 所有[GDB]的文档都随机器可读分发一起提供。文档采用Texinfo格式书写，这是一种使用单一源文件来产生在线信息和印刷版手册的文档系统。您可以使用Info格式化命令之一来创建文档的在线版本，并使用TeX（或“texi2roff”）来排版印刷版本。

[GDB] Texinfo distribution.


If you want to format these Info files yourself, you need one of the Info formatting programs, such as `texinfo-format-buffer` or `makeinfo`.

> 如果你想自己格式化这些信息文件，你需要一个信息格式化程序，比如`texinfo-format-buffer`或`makeinfo`。


If you have `makeinfo` installed, and are in the top level [GDB], in the case of version 14.0.50.20230622-git), you can make the Info file by typing:

> 如果你已经安装了 `makeinfo`，并且位于[GDB]的顶层（例如14.0.50.20230622-git的版本），你可以通过输入以下命令来制作Info文件：

::: smallexample

```bash
cd gdb
make gdb.info
```

:::


If you want to typeset and print copies of this manual, you need TeX, a program to print its [DVI], the Texinfo definitions file.

> 如果你想要排版和打印这份手册的副本，你需要TeX，一个用来打印它的DVI的程序，以及Texinfo定义文件。


TeX is a typesetting program; it does not print files directly, but produces output files called [DVI]' extension.

> TeX 是一个排版程序；它不能直接打印文件，而是产生后缀名为[DVI]的输出文件。


TeX also requires a macro definitions file called `texinfo.tex` directory.

> TeX 需要一个叫做`texinfo.tex`的宏定义文件存放在目录中。

If you have TeX and a [DVI]) and type:

::: smallexample

```bash
make gdb.dvi
```

:::

Then give `gdb.dvi` printing program.

::: footnote

---

#### Footnotes

### [(21)](#DOCF21)


In `gdb-14.0.50.20230622-git/gdb/refcard.ps` of the version 14.0.50.20230622-git release.

> 在14.0.50.20230622-git版本的gdb-14.0.50.20230622-git/gdb/refcard.ps中。
:::

---

::: header
Next: [Installing GDB](Installing-GDB.html#Installing-GDB)]
:::
