---
tip: translate by openai@2023-06-23 16:59:26
...
---
description: Ada Source Character Set (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Ada Source Character Set (Debugging with GDB)
lang: en
resource-type: document
title: Ada Source Character Set (Debugging with GDB)
---
::: header
Next: [Ada Glitches](Ada-Glitches.html#Ada-Glitches)]
:::

---

#### 15.4.10.10 Ada Source Character Set


The GNAT compiler supports a number of character sets for source files. See [(gnat_ugn)Character Set Control](http://gcc.gnu.org/onlinedocs/gnat_ugn/Character-Set-Control.html#Character-Set-Control). [GDB] includes support for this as well.

> GNAT编译器支持多种字符集的源文件。请参阅[(gnat_ugn)字符集控制](http://gcc.gnu.org/onlinedocs/gnat_ugn/Character-Set-Control.html#Character-Set-Control)。[GDB]也支持此功能。

`set ada source-charset charset`

:

```
Set the source character set for Ada. The character set must be supported by GNAT. Because this setting affects the decoding of symbols coming from the debug information in your program, the setting should be set as early as possible. The default is `ISO-8859-1`, because that is also GNAT's default.
```

`show ada source-charset`

:

```
Show the current source character set for Ada.
```
