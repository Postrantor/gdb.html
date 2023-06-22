---
description: Summary (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Summary (Debugging with GDB)
lang: en
resource-type: document
title: Summary (Debugging with GDB)
---
::: header
Next: [Sample Session](Sample-Session.html#Sample-Session)]
:::

---

## Summary of [GDB]

The purpose of a debugger such as [GDB] is to allow you to see what is going on "inside" another program while it executes---or what another program was doing at the moment it crashed.

[GDB] can do four main kinds of things (plus other things in support of these) to help you catch bugs in the act:

- Start your program, specifying anything that might affect its behavior.
- Make your program stop on specified conditions.
- Examine what has happened, when your program has stopped.
- Change things in your program, so you can experiment with correcting the effects of one bug and go on to learn about another.

You can use [GDB] to debug programs written in C and C++. For more information, see [Supported Languages](Supported-Languages.html#Supported-Languages). For more information, see [C and C++](C.html#C).

Support for D is partial. For information on D, see [D](D.html#D).

Support for Modula-2 is partial. For information on Modula-2, see [Modula-2](Modula_002d2.html#Modula_002d2).

Support for OpenCL C is partial. For information on OpenCL C, see [OpenCL C](OpenCL-C.html#OpenCL-C).

Debugging Pascal programs which use sets, subranges, file variables, or nested functions does not currently work. [GDB] does not support entering expressions, printing values, or similar features using Pascal syntax.

[GDB] can be used to debug programs written in Fortran, although it may be necessary to refer to some variables with a trailing underscore.

[GDB] can be used to debug programs written in Objective-C, using either the Apple/NeXT or the GNU Objective-C runtime.

---

• [Free Software](Free-Software.html#Free-Software):                       Freely redistributable software
• [Free Documentation](Free-Documentation.html#Free-Documentation):        Free Software Needs Free Documentation
• [Contributors](Contributors.html#Contributors):                          Contributors to GDB

---

---

::: header
Next: [Sample Session](Sample-Session.html#Sample-Session)]
:::
