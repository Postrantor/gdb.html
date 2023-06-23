---
description: Enum Target Types (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Enum Target Types (Debugging with GDB)
lang: en
resource-type: document
title: Enum Target Types (Debugging with GDB)
---
::: header
Next: [Standard Target Features](Standard-Target-Features.html#Standard-Target-Features)]
:::

---

### G.4 Enum Target Types

Enum target types are useful in '`struct`' register descriptions. See [Target Description Format](Target-Description-Format.html#Target-Description-Format).

Enum types have a name, size and a list of name/value pairs.

::: smallexample

```bash
<enum id="id" size="size">
  <evalue name="name" value="value"/>
  …
</enum>
```

:::

Enums must be defined before they are used.

::: smallexample

```bash
<enum id="levels_type" size="4">
  <evalue name="low" value="0"/>
  <evalue name="high" value="1"/>
</enum>
<flags id="flags_type" size="4">
  <field name="X" start="0"/>
  <field name="LEVEL" start="1" end="1" type="levels_type"/>
</flags>
<reg name="flags" bitsize="32" type="flags_type"/>
```

:::

Given that description, a value of 3 for the '`flags`' register would be printed as:

::: smallexample

```bash
(gdb) info register flags
flags 0x3 [ X LEVEL=high ]
```

:::
