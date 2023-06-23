---
description: Darwin (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Darwin (Debugging with GDB)
lang: en
resource-type: document
title: Darwin (Debugging with GDB)
---
::: header
Next: [FreeBSD](FreeBSD.html#FreeBSD)]
:::

---

#### 21.1.6 Darwin

[GDB] provides the following commands specific to the Darwin target:

`set debug darwin num`

:

```
When set to a non zero value, enables debugging messages specific to the Darwin support. Higher values produce more verbose output.
```

`show debug darwin`

:

```
Show the current state of Darwin messages.
```

`set debug mach-o num`

:

```
When set to a non zero value, enables debugging messages while [GDB] and should not be needed in normal usage.
```

`show debug mach-o`

:

```
Show the current state of Mach-O file messages.
```

`set mach-exceptions on`
`set mach-exceptions off`

:

```
On Darwin, faults are first reported as a Mach exception and are then mapped to a Posix signal. Use this command to turn on trapping of Mach exceptions in the inferior. This might be sometimes useful to better understand the cause of a fault. The default is off.
```

`show mach-exceptions`

:

```
Show the current state of exceptions trapping.
```
