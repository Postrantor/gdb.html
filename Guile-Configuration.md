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

```
<!-- -->
```

Scheme Procedure: **target-config**

:   Return a string containing the target configuration. This is the string passed to `--target` when [GDB] was configured.
