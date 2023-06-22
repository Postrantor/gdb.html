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

You can build the test program using the `d10v-elf` GCC cross-compiler like this:

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
