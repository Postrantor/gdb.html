---
tip: translate by openai@2023-06-23 23:43:58
...
---
description: I/O Ports in Guile (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: I/O Ports in Guile (Debugging with GDB)
lang: en
resource-type: document
title: I/O Ports in Guile (Debugging with GDB)
---
::: header
Next: [Memory Ports in Guile](Memory-Ports-in-Guile.html#Memory-Ports-in-Guile)]
:::

---

#### 23.4.3.23 I/O Ports in Guile

Scheme Procedure: **input-port**

:   Return [GDB]'s input port as a Guile port object.

```
<!-- -->
```

Scheme Procedure: **output-port**

:   Return [GDB]'s output port as a Guile port object.

```
<!-- -->
```

Scheme Procedure: **error-port**

:   Return [GDB]'s error port as a Guile port object.

```
<!-- -->
```

Scheme Procedure: **stdio-port?** *object*

:   Return `#t` if `object` stdio port. Otherwise return `#f`.
