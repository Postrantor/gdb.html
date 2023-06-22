---
description: Automatic Overlay Debugging (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Automatic Overlay Debugging (Debugging with GDB)
lang: en
resource-type: document
title: Automatic Overlay Debugging (Debugging with GDB)
---
::: header
Next: [Overlay Sample Program](Overlay-Sample-Program.html#Overlay-Sample-Program)]
:::

---

### 14.3 Automatic Overlay Debugging

[GDB] looks in the inferior's memory for certain variables describing the current state of the overlays.

Here are the variables your overlay manager must define to support [GDB]'s automatic overlay debugging:

`_ovly_table`:

:   This variable must be an array of the following structures:

```
::: smallexample
``` smallexample
struct
{
  /* The overlay's mapped address.  */
  unsigned long vma;

  /* The size of the overlay, in bytes.  */
  unsigned long size;

  /* The overlay's load address.  */
  unsigned long lma;

  /* Non-zero if the overlay is currently mapped;
     zero otherwise.  */
  unsigned long mapped;
}
```

:::

```

`_novlys`:

:   This variable must be a four-byte signed integer, holding the total number of elements in `_ovly_table`.

To decide whether a particular overlay is mapped or not, [GDB] finds a matching entry, it consults the entry's `mapped` member to determine whether the overlay is currently mapped.

In addition, your overlay manager may define a function called `_ovly_debug_event`. If this function is defined, [GDB] to accurately keep track of which overlays are in program memory, and update any breakpoints that may be set in overlays. This will allow breakpoints to work even if the overlays are kept in ROM or other non-writable memory while they are not being executed.

---

::: header
Next: [Overlay Sample Program](Overlay-Sample-Program.html#Overlay-Sample-Program)]
:::
```
