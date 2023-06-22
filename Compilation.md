---
description: Compilation (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Compilation (Debugging with GDB)
lang: en
resource-type: document
title: Compilation (Debugging with GDB)
---
::: header
Next: [Starting](Starting.html#Starting)]
:::

---

### 4.1 Compiling for Debugging

In order to debug a program effectively, you need to generate debugging information when you compile it. This debugging information is stored in the object file; it describes the data type of each variable or function and the correspondence between source line numbers and addresses in the executable code.

To request debugging information, specify the '`-g`' option when you run the compiler.

Programs that are to be shipped to your customers are compiled with optimizations, using the '`-O`' options together. Using those compilers, you cannot generate optimized executables containing debugging information.

[GCC]' whenever you compile a program. You may think your program is correct, but there is no sense in pushing your luck. For more information, see [Optimized Code](Optimized-Code.html#Optimized-Code).

Older versions of the [GNU] C compiler has this option, do not use it.

[GDB].

See [Options for Debugging Your Program or GCC](http://gcc.gnu.org/onlinedocs/gcc/Debugging-Options.html#Debugging-Options) in Using the [GNU] options affecting debug information.

You will have the best debugging experience if you use the latest version of the DWARF debugging format that your compiler supports. DWARF is currently the most expressive and best supported debugging format in [GDB].

---

::: header
Next: [Starting](Starting.html#Starting)]
:::
