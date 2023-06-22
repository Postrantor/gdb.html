---
description: Annotations Overview (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Annotations Overview (Debugging with GDB)
lang: en
resource-type: document
title: Annotations Overview (Debugging with GDB)
---
::: header
Next: [Server Prefix](Server-Prefix.html#Server-Prefix)]
:::

---

### 28.1 What is an Annotation?

Annotations start with a newline character, two '`control-z`' characters, and the name of the annotation. If there is no additional information associated with this annotation, the name of the annotation is followed immediately by a newline. If there is additional information, the name of the annotation is followed by a space, the additional information, and a newline. The additional information cannot contain newline characters.

Any output not beginning with a newline and two '`control-z`' annotation which means those three characters as output.

The annotation `level`, and level 2 annotations have been made obsolete (see [Limitations of the Annotation Interface](../annotate/Limitations.html#Limitations) in GDB's Obsolete Annotations).

`set annotate level`

The [GDB].

`show annotate`

Show the current annotation level.

This chapter describes level 3 annotations.

A simple example of starting up [GDB] with annotations is:

::: smallexample

```bash
$ gdb --annotate=3
GNU gdb 6.0
Copyright 2003 Free Software Foundation, Inc.
GDB is free software, covered by the GNU General Public License,
and you are welcome to change it and/or distribute copies of it
under certain conditions.
Type "show copying" to see the conditions.
There is absolutely no warranty for GDB.  Type "show warranty"
for details.
This GDB was configured as "i386-pc-linux-gnu"

^Z^Zpre-prompt
(gdb)
^Z^Zprompt
quit

^Z^Zpost-prompt
$
```

:::

Here '`quit`.

---

::: header
Next: [Server Prefix](Server-Prefix.html#Server-Prefix)]
:::
