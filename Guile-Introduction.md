---
description: Guile Introduction (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Guile Introduction (Debugging with GDB)
lang: en
resource-type: document
title: Guile Introduction (Debugging with GDB)
---
::: header
Next: [Guile Commands](Guile-Commands.html#Guile-Commands)]
:::

---

#### 23.4.1 Guile Introduction

Guile is an implementation of the Scheme programming language and is the GNU project's official extension language.

Guile support in [GDB] reasonably closely, so concepts there should carry over. However, some things are done differently where it makes sense.

[GDB] requires Guile version 3.0, 2.2, or 2.0.

Guile scripts used by [GDB] startup (see [Data Files](Data-Files.html#Data-Files)). This directory, known as the *guile directory*, is automatically added to the Guile Search Path in order to allow the Guile interpreter to locate all scripts installed at this location.
