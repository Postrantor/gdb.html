---
tip: translate by openai@2023-06-23 23:01:36
...
---
description: Guile Configuration (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Guile Configuration (Debugging with GDB)
lang: en
resource-type: document
title: Guile Configuration (Debugging with GDB)
---
::: header
Next: [GDB Scheme Data Types](GDB-Scheme-Data-Types.html#GDB-Scheme-Data-Types)]
:::

---

#### 23.4.3.2 Guile Configuration


[GDB] provides these Scheme functions to access various configuration parameters.

> [GDB]提供这些Scheme函数来访问各种配置参数。

Scheme Procedure: **data-directory**

:   Return a string containing [GDB]'s ancillary files.

```
<!-- -->
```

Scheme Procedure: **guile-data-directory**

:   Return a string containing [GDB].

```
<!-- -->
```

Scheme Procedure: **gdb-version**

:   Return a string containing the [GDB] version.

```
<!-- -->
```

Scheme Procedure: **host-config**


:   Return a string containing the host configuration. This is the string passed to `--host` when [GDB] was configured.

> 返回一个包含主机配置的字符串。这是传递给`--host`的字符串，当[GDB]进行配置时。

```
<!-- -->
```

Scheme Procedure: **target-config**


:   Return a string containing the target configuration. This is the string passed to `--target` when [GDB] was configured.

> 返回一个包含目标配置的字符串。这是在配置[GDB]时传递给`--target`的字符串。
