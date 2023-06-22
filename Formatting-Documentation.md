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

::: smallexample

```bash
make refcard.dvi
```

:::

The [GDB] output program.

All the documentation for [GDB] comes as part of the machine-readable distribution. The documentation is written in Texinfo format, which is a documentation system that uses a single source file to produce both on-line information and a printed manual. You can use one of the Info formatting commands to create the on-line version of the documentation and TeX (or `texi2roff`) to typeset the printed version.

[GDB] Texinfo distribution.

If you want to format these Info files yourself, you need one of the Info formatting programs, such as `texinfo-format-buffer` or `makeinfo`.

If you have `makeinfo` installed, and are in the top level [GDB], in the case of version 14.0.50.20230622-git), you can make the Info file by typing:

::: smallexample

```bash
cd gdb
make gdb.info
```

:::

If you want to typeset and print copies of this manual, you need TeX, a program to print its [DVI], the Texinfo definitions file.

TeX is a typesetting program; it does not print files directly, but produces output files called [DVI]' extension.

TeX also requires a macro definitions file called `texinfo.tex` directory.

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
:::

---

::: header
Next: [Installing GDB](Installing-GDB.html#Installing-GDB)]
:::
