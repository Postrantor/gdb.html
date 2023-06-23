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

Alternatively, you can specify a file to read for the target description. If a file is set, the target will not be queried. The commands to specify a file are:

`set tdesc filename path`

Read the target description from `path`.

`unset tdesc filename`

Do not read the XML target description from a file. [GDB] will use the description supplied by the current target.

`show tdesc filename`

Show the filename to read for a target description, if any.
