---
description: Target Description Format (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Target Description Format (Debugging with GDB)
lang: en
resource-type: document
title: Target Description Format (Debugging with GDB)
---
::: header
Next: [Predefined Target Types](Predefined-Target-Types.html#Predefined-Target-Types)]
:::

---

### G.2 Target Description Format

A target description annex is an [XML](http://www.w3.org/XML/) document which complies with the Document Type Definition provided in the [GDB]. This means you can use generally available tools like `xmllint` to check that your feature descriptions are well-formed and valid. However, to help people unfamiliar with XML write descriptions for their targets, we also describe the grammar here.

Target descriptions can identify the architecture of the remote target and (for some architectures) provide information about custom register sets. They can also identify the OS ABI of the remote target. [GDB] can use this information to autoconfigure for your target, or to warn you if you connect to an unsupported target.

Here is a simple target description:

::: smallexample

```bash
<target version="1.0">
  <architecture>i386:x86-64</architecture>
</target>
```

:::

This minimal description only says that the target uses the x86-64 architecture.

A target description has the following overall form, with \[ ] marking optional elements and ... marking repeatable elements. The elements are explained further below.

::: smallexample

```bash
<?xml version="1.0"?>
<!DOCTYPE target SYSTEM "gdb-target.dtd">
<target version="1.0">
  [architecture]
  [osabi]
  [compatible]
  [feature…]
</target>
```

:::

The description is generally insensitive to whitespace and line breaks, under the usual common-sense rules. The XML version declaration and document type declaration can generally be omitted ([GDB], they will detect and report the version mismatch.

#### G.2.1 Inclusion

It can sometimes be valuable to split a target description up into several different annexes, either for organizational purposes, or to share files between different possible target descriptions. You can divide a description into multiple files by replacing any element of the target description with an inclusion directive of the form:

::: smallexample

```bash
<xi:include href="document"/>
```

:::

When [GDB] as a file in the same directory where it found the original description.

#### G.2.2 Architecture

An '`<architecture>`' element has this form:

::: smallexample

```bash
  <architecture>arch</architecture>
```

:::

`arch` is one of the architectures from the set accepted by `set architecture` (see [Specifying a Debugging Target](Targets.html#Targets)).

#### G.2.3 OS ABI

This optional field was introduced in [GDB] ignore it.

An '`<osabi>`' element has this form:

::: smallexample

```bash
  <osabi>abi-name</osabi>
```

:::

`abi-name` is an OS ABI name from the same selection accepted by `set osabi` (see [Configuring the Current ABI](ABI.html#ABI)).

#### G.2.4 Compatible Architecture

This optional field was introduced in [GDB] ignore it.

A '`<compatible>`' element has this form:

::: smallexample

```bash
  <compatible>arch</compatible>
```

:::

`arch` is one of the architectures from the set accepted by `set architecture` (see [Specifying a Debugging Target](Targets.html#Targets)).

A '`<compatible>`' is as follows:

::: smallexample

```bash
  <architecture>powerpc:common</architecture>
  <compatible>spu</compatible>
```

:::

#### G.2.5 Features

Each '`<feature>`' element has this form:

::: smallexample

```bash
<feature name="name">
  [type…]
  reg…
</feature>
```

:::

Each feature's name should be unique within the description. The name of a feature does not matter unless [GDB] has some special knowledge of the contents of that feature; if it does, the feature should have its standard name. See [Standard Target Features](Standard-Target-Features.html#Standard-Target-Features).

#### G.2.6 Types

Any register's value is a collection of bits which [GDB] (see [Predefined Target Types](Predefined-Target-Types.html#Predefined-Target-Types)), and the description can define additional composite and enum types.

Each type element must have an '`id`') name to the type. Types must be defined before they are used.

Some targets offer vector registers, which can be treated as arrays of scalar elements. These types are written as '`<vector>`:

::: smallexample

```bash
<vector id="id" type="type" count="count"/>
```

:::

If a register's value is usefully viewed in multiple ways, define it with a union type containing the useful representations. The '`<union>`:

::: smallexample

```bash
<union id="id">
  <field name="name" type="type"/>
  …
</union>
```

:::

If a register's value is composed from several separate values, define it with either a structure type or a flags type. A flags type may only contain bitfields. A structure type may either contain only bitfields or contain no bitfields. If the value contains only bitfields, its total size in bytes must be specified.

Non-bitfield values have a `name`.

::: smallexample

```bash
<struct id="id">
  <field name="name" type="type"/>
  …
</struct>
```

:::

Both `name` values are required. No implicit padding is added.

Bitfield values have a `name`.

::: smallexample

```bash
<struct id="id" size="size">
  <field name="name" start="start" end="end" type="type"/>
  …
</struct>
```

:::

::: smallexample

```bash
<flags id="id" size="size">
  <field name="name" start="start" end="end" type="type"/>
  …
</flags>
```

:::

The `name`', in which case the field is "filler" and its value is not printed. Not all bits need to be specified, so "filler" fields are optional.

The `start`, and zero represents the least significant bit.

The default value of `type` is `bool` for single bit fields, and an unsigned integer otherwise.

Which to choose? Structures or flags?

Registers defined with '`flags`':

- Arithmetic may be performed on them as if they were integers.
- They are printed in a more readable fashion.

Registers defined with '`struct`':

- One can fetch individual fields like in '`C`'.

  ::: smallexample

  ```bash
  (gdb) print $my_struct_reg.field3
  $1 = 42
  ```

  :::

#### G.2.7 Registers

Each register is represented as an element with this form:

::: smallexample

```bash
<reg name="name"
     bitsize="size"
     [regnum="num"]
     [save-restore="save-restore"]
     [type="type"]
     [group="group"]/>
```

:::

The components are as follows:

`name`

:   The register's name; it must be unique within the target description.

`bitsize`

:   The register's size, in bits.

`regnum`

:   The register's number. If omitted, a register's number is one greater than that of the previous register (either in the current feature or in a preceding feature); the first register in the target description defaults to zero. This register number is used to read or write the register; e.g. it is used in the remote `p` and `P` packets, and registers appear in the `g` and `G` packets in order of increasing register number.

`save-restore`

:   Whether the register should be preserved across inferior function calls; this must be either `yes` or `no`. The default is `yes`, which is appropriate for most registers except for some system control registers; this is not related to the target's ABI.

`type`

:   The type of the register. It may be a predefined type, a type defined in the current feature, or one of the special types `int` and `float`. `int` is an integer type of the correct size for `bitsize`. The default is `int`.

`group`

:   The register group to which this register belongs. It can be one of the standard register groups `general`, `float`, `vector` or an arbitrary string. Group names should be limited to alphanumeric characters. If a group name is made up of multiple words the words may be separated by hyphens; e.g. `special-group` or `ultra-special-group`. If no `group` will not display the register in `info registers`.

---

::: header
Next: [Predefined Target Types](Predefined-Target-Types.html#Predefined-Target-Types)]
:::
