---
tip: translate by openai@2023-06-23 23:03:16
...
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

> Guile是Scheme编程语言的一种实现，是GNU项目的官方扩展语言。


Guile support in [GDB] reasonably closely, so concepts there should carry over. However, some things are done differently where it makes sense.

> GDB中的Guile支持相当紧密，因此那里的概念应该可以搬运过来。但是，在有意义的地方，有些事情是有所不同的。

[GDB] requires Guile version 3.0, 2.2, or 2.0.


Guile scripts used by [GDB] startup (see [Data Files](Data-Files.html#Data-Files)). This directory, known as the *guile directory*, is automatically added to the Guile Search Path in order to allow the Guile interpreter to locate all scripts installed at this location.

> GDB 启动时使用的 Guile 脚本（参见 [数据文件](Data-Files.html#Data-Files)）。这个目录，也称为 guile 目录，会自动添加到 Guile 搜索路径中，以便 Guile 解释器找到此位置安装的所有脚本。
