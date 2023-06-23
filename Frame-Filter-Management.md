---
description: Frame Filter Management (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Frame Filter Management (Debugging with GDB)
lang: en
resource-type: document
title: Frame Filter Management (Debugging with GDB)
---
::: header
Previous: [Frame Apply](Frame-Apply.html#Frame-Apply)]
:::

---

### 8.6 Management of Frame Filters.

Frame filters are Python based utilities to manage and decorate the output of frames. See [Frame Filter API](Frame-Filter-API.html#Frame-Filter-API), for further information.

Managing frame filters is performed by several commands available within [GDB], detailed here.

`info frame-filter`

Print a list of installed frame filters from all dictionaries, showing their name, priority and enabled status.

`disable frame-filter filter-dictionary filter-name`

Disable a frame filter in the dictionary matching `filter-dictionary`. A disabled frame-filter is not deleted, it may be enabled again later.

`enable frame-filter filter-dictionary filter-name`

Enable a frame filter in the dictionary matching `filter-dictionary`.

Example:

::: smallexample

```bash
(gdb) info frame-filter

global frame-filters:
  Priority  Enabled  Name
  1000      No       PrimaryFunctionFilter
  100       Yes      Reverse

progspace /build/test frame-filters:
  Priority  Enabled  Name
  100       Yes      ProgspaceFilter

objfile /build/test frame-filters:
  Priority  Enabled  Name
  999       Yes      BuildProgramFilter

(gdb) disable frame-filter /build/test BuildProgramFilter
(gdb) info frame-filter

global frame-filters:
  Priority  Enabled  Name
  1000      No       PrimaryFunctionFilter
  100       Yes      Reverse

progspace /build/test frame-filters:
  Priority  Enabled  Name
  100       Yes      ProgspaceFilter

objfile /build/test frame-filters:
  Priority  Enabled  Name
  999       No       BuildProgramFilter

(gdb) enable frame-filter global PrimaryFunctionFilter
(gdb) info frame-filter

global frame-filters:
  Priority  Enabled  Name
  1000      Yes      PrimaryFunctionFilter
  100       Yes      Reverse

progspace /build/test frame-filters:
  Priority  Enabled  Name
  100       Yes      ProgspaceFilter

objfile /build/test frame-filters:
  Priority  Enabled  Name
  999       No       BuildProgramFilter
```

:::

`set frame-filter priority filter-dictionary filter-name priority`

Set the `priority` is an integer.

`show frame-filter priority filter-dictionary filter-name`

Show the `priority` may be `global`, `progspace` or the name of the object file where the frame filter dictionary resides.

Example:

::: smallexample

```bash
(gdb) info frame-filter

global frame-filters:
  Priority  Enabled  Name
  1000      Yes      PrimaryFunctionFilter
  100       Yes      Reverse

progspace /build/test frame-filters:
  Priority  Enabled  Name
  100       Yes      ProgspaceFilter

objfile /build/test frame-filters:
  Priority  Enabled  Name
  999       No       BuildProgramFilter

(gdb) set frame-filter priority global Reverse 50
(gdb) info frame-filter

global frame-filters:
  Priority  Enabled  Name
  1000      Yes      PrimaryFunctionFilter
  50        Yes      Reverse

progspace /build/test frame-filters:
  Priority  Enabled  Name
  100       Yes      ProgspaceFilter

objfile /build/test frame-filters:
  Priority  Enabled  Name
  999       No       BuildProgramFilter
```

:::

---

::: header
Previous: [Frame Apply](Frame-Apply.html#Frame-Apply)]
:::
