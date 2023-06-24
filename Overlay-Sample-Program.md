---
tip: translate by openai@2023-06-24 00:56:51
...
---
description: Overlay Sample Program (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Overlay Sample Program (Debugging with GDB)
lang: en
resource-type: document
title: Overlay Sample Program (Debugging with GDB)
---
::: header
Previous: [Automatic Overlay Debugging](Automatic-Overlay-Debugging.html#Automatic-Overlay-Debugging)]
:::

---

### 14.4 Overlay Sample Program


When linking a program which uses overlays, you must place the overlays at their load addresses, while relocating them to run at their mapped addresses. To do this, you must write a linker script (see [Overlay Description](http://sourceware.org/binutils/docs/ld/Overlay-Description.html#Overlay-Description) in Using ld: the GNU linker). Unfortunately, since linker scripts are specific to a particular host system, target architecture, and target memory layout, this manual cannot provide portable sample code demonstrating [GDB]'s overlay support.

> 当链接一个使用覆盖的程序时，您必须将覆盖放置在其加载地址，同时将其重定位到其映射地址运行。为此，您必须编写链接器脚本（请参见使用ld：GNU链接器中的[覆盖描述]（http://sourceware.org/binutils/docs/ld/Overlay-Description.html#Overlay-Description））。不幸的是，由于链接器脚本是特定于特定主机系统，目标体系结构和目标内存布局的，本手册无法提供用于演示[GDB]覆盖支持的可移植样例代码。

However, the [GDB]:

`overlays.c`

:   The main program file.

`ovlymgr.c`

:   A simple overlay manager, used by `overlays.c`.

`foo.c`
`bar.c`
`baz.c`
`grbx.c`

:   Overlay modules, loaded and used by `overlays.c`.

`d10v.ld`
`m32r.ld`


:   Linker scripts for linking the test program on the `d10v-elf` and `m32r-elf` targets.

> 链接测试程序到`d10v-elf`和`m32r-elf`目标上所需的链接器脚本。


You can build the test program using the `d10v-elf` GCC cross-compiler like this:

> 你可以使用`d10v-elf` GCC交叉编译器像这样构建测试程序：

::: smallexample

```bash
$ d10v-elf-gcc -g -c overlays.c
$ d10v-elf-gcc -g -c ovlymgr.c
$ d10v-elf-gcc -g -c foo.c
$ d10v-elf-gcc -g -c bar.c
$ d10v-elf-gcc -g -c baz.c
$ d10v-elf-gcc -g -c grbx.c
$ d10v-elf-gcc -g overlays.o ovlymgr.o foo.o bar.o \
                  baz.o grbx.o -Wl,-Td10v.ld -o overlays
```

:::


The build process is identical for any other architecture, except that you must substitute the appropriate compiler and linker script for the target system for `d10v-elf-gcc` and `d10v.ld`.

> 编译过程对于任何其他架构都是相同的，只需要替换目标系统的适当编译器和链接器脚本，替换为`d10v-elf-gcc`和`d10v.ld`。
